pipeline {
    agent any  // Use any available agent for the pipeline

    environment {
        DOCKER_IMAGE = 'admin/docker-plugin'  
        DOCKER_TAG = 'latest'  
        DOCKER_CREDENTIALS = 'dockerhub-credentials'  
    }

    stages {
        stage('Checkout') {
            steps {
              
                git branch: 'main', url: 'https://github.com/RajbeerChauhan/my-app'
            }
        }
        
     
    

         stage('Build Docker Image') {
            steps {
                script {
                    
                    sh 'docker build -t my-app .'
                }
            }
        }



        stage('Push Docker Image') {
            steps {
                script {
                    
                    withCredentials([usernamePassword(credentialsId: DOCKER_CREDENTIALS, usernameVariable: 'admin', passwordVariable: 'admin')]) {
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
            
            cleanWs()
        }
    }
}
