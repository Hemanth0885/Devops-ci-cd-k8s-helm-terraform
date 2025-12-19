pipeline {
    agent any

    environment {
        DOCKER_HUB_CREDENTIALS = 'dockerhub-creds' // Jenkins creds id
        DOCKER_HUB_USERNAME = 'he40133895'         // username
        IMAGE_NAME = 'sampleapp'
        IMAGE_TAG = '1.0'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Hemanth0885/Devops-ci-cd-k8s-helm-terraform.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh """
                   docker build \
                   -t ${DOCKER_HUB_USERNAME}/${IMAGE_NAME}:${IMAGE_TAG} \
                   ./app/sampleapp/sampleapp
                """
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: "${DOCKER_HUB_CREDENTIALS}",
                    usernameVariable: 'USERNAME',
                    passwordVariable: 'PASSWORD'
                )]) {
                    sh """
                       echo "$PASSWORD" | docker login -u "$USERNAME" --password-stdin
                       docker push ${DOCKER_HUB_USERNAME}/${IMAGE_NAME}:${IMAGE_TAG}
                    """
                }
            }
        }
    }

    post {
        success {
            echo "Docker image pushed successfully to Docker Hub"
        }
        failure {
            echo "Pipeline failed"
        }
    }
}
