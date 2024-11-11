pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/your-repo/my-app'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image
                    sh 'docker build -t my-app .'
                }
            }
        }

        stage('Run Tests in Docker') {
            steps {
                script {
                    // Run tests inside the Docker container
                    sh 'docker run my-app ./run-tests.sh'
                }
            }
        }

        stage('Deploy to Docker Hub') {
            steps {
                script {
                    // Log in to Docker Hub and push the image
                    sh 'docker login -u $DOCKER_USER -p $DOCKER_PASSWORD'
                    sh 'docker push my-app'
                }
            }
        }
    }
}
