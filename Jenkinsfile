pipeline {
    agent any

    environment {
        DOCKER_HUB_CREDENTIALS = 'dockerhub-creds' // Jenkins credentials ID
        DOCKER_HUB_USERNAME = 'he40133895'         // Your Docker Hub username
        IMAGE_NAME = 'sampleapp'
        IMAGE_TAG = '1.0'
    }

    stages {
        stage('Checkout') {
            steps {
                // Clone the GitHub repo
                git branch: 'main', url: 'https://github.com/<your-username>/<repo-name>.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image from app folder
                    sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ./app"
                }
            }
        }

        stage('Tag Image') {
            steps {
                script {
                    sh "docker tag ${IMAGE_NAME}:${IMAGE_TAG} ${DOCKER_HUB_USERNAME}/${IMAGE_NAME}:${IMAGE_TAG}"
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    // Login to Docker Hub using credentials stored in Jenkins
                    withCredentials([usernamePassword(credentialsId: "${DOCKER_HUB_CREDENTIALS}", 
                                                     usernameVariable: 'USERNAME', 
                                                     passwordVariable: 'PASSWORD')]) {
                        sh "echo $PASSWORD | docker login -u $USERNAME --password-stdin"
                        sh "docker push ${DOCKER_HUB_USERNAME}/${IMAGE_NAME}:${IMAGE_TAG}"
                    }
                }
            }
        }
    }

    post {
        always {
            echo "Pipeline finished"
        }
        success {
            echo "Docker image pushed successfully!"
        }
        failure {
            echo "Something went wrong!"
        }
    }
}
