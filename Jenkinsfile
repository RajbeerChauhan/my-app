pipeline {
    agent any  // Use any available agent for the pipeline

    environment {
        DOCKER_IMAGE = 'your-dockerhub-username/your-image-name'  // Replace with your Docker Hub username/repository name
        DOCKER_TAG = 'latest'  // Or dynamically set it based on Git commit, build number, etc.
        DOCKER_CREDENTIALS = 'dockerhub-credentials'  // The credentials ID you saved in Jenkins for Docker Hub
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from GitHub
                git branch: 'main', url: 'https://github.com/your-username/your-repo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image with the tag "latest"
                    sh 'docker build -t $DOCKER_IMAGE:$DOCKER_TAG .'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    // Log in to Docker Hub and push the image
                    withCredentials([usernamePassword(credentialsId: DOCKER_CREDENTIALS, usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        sh """
                            echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin
                            docker push $DOCKER_IMAGE:$DOCKER_TAG
                        """
                    }
                }
            }
        }
    }

    post {
        always {
            // Clean workspace after build
            cleanWs()
        }
    }
}

