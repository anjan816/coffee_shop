pipeline {
agent any

```
environment {
    IMAGE_NAME = "coffee_shop"
    IMAGE_TAG = "${BUILD_NUMBER}"
}

stages {

    stage('Checkout') {
        steps {
            checkout scm
        }
    }

    stage('Test HTML') {
        steps {
            sh '''
                echo "Validating HTML..."
                docker run --rm \
                -v $(pwd):/workspace \
                node:18-alpine \
                sh -c "npm install -g htmlhint && htmlhint /workspace/index.html"
            '''
        }
    }

    stage('Build Docker Image') {
        steps {
            sh '''
                docker build -t $IMAGE_NAME:$IMAGE_TAG .
            '''
        }
    }

    stage('Docker Login') {
        steps {
            withCredentials([
                usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )
            ]) {
                sh '''
                    echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                '''
            }
        }
    }

    stage('Push Image') {
        steps {
            sh '''
                docker push $IMAGE_NAME:$IMAGE_TAG
                docker tag $IMAGE_NAME:$IMAGE_TAG $IMAGE_NAME:latest
                docker push $IMAGE_NAME:latest
            '''
        }
    }

    stage('Deploy Container') {
        steps {
            sh '''
                docker stop html-app || true
                docker rm html-app || true

                docker run -d \
                    --name html-app \
                    -p 80:80 \
                    $IMAGE_NAME:$IMAGE_TAG
            '''
        }
    }
}

post {
    success {
        echo 'Pipeline completed successfully!'
    }

    failure {
        echo 'Pipeline failed!'
    }
}
```

}
