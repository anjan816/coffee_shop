pipeline {
    agent any

    environment {
        IMAGE_NAME = "coffee_shop"
        DOCKER_HUB_USERNAME = "YOUR_DOCKERHUB_USERNAME"
        IMAGE_TAG = "${BUILD_NUMBER}"
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

       

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t $DOCKER_HUB_USERNAME/$IMAGE_NAME:$IMAGE_TAG .
                docker tag $DOCKER_HUB_USERNAME/$IMAGE_NAME:$IMAGE_TAG \
                           $DOCKER_HUB_USERNAME/$IMAGE_NAME:latest
                '''
            }
        }

        stage('Login Docker Hub') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-creds',
                        usernameVariable: 'DOCKER_USERNAME',
                        passwordVariable: 'DOCKER_PASSWORD'
                    )
                ]) {
                    sh '''
                    echo "$DOCKER_PASSWORD" | docker login \
                    -u "$DOCKER_USERNAME" \
                    --password-stdin
                    '''
                }
            }
        }

        stage('Push Image') {
            steps {
                sh '''
                docker push $DOCKER_HUB_USERNAME/$IMAGE_NAME:$IMAGE_TAG
                docker push $DOCKER_HUB_USERNAME/$IMAGE_NAME:latest
                '''
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                docker stop coffee-container || true
                docker rm coffee-container || true

                docker pull $DOCKER_HUB_USERNAME/$IMAGE_NAME:latest

                docker run -d \
                --name coffee-container \
                -p 80:80 \
                $DOCKER_HUB_USERNAME/$IMAGE_NAME:latest
                '''
            }
        }
    }

    post {
        success {
            echo 'CI/CD Pipeline Executed Successfully!'
        }

        failure {
            echo 'Pipeline Failed!'
        }
    }
}
