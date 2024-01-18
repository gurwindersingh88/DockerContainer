pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'your-docker-registry/your-docker-image:latest'
        CONTAINER_NAME = 'your-container'
        PORT_MAPPING = '8080:80'
        DOCKER_PATH = 'C:/Program Files/Docker/Docker/resources/bin/docker.exe' // Replace with the actual path to your Docker executable
    }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image using the full path to Docker executable
                    sh "${DOCKER_PATH} build -t ${DOCKER_IMAGE} ."
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    // Push Docker image to registry
                    sh "${DOCKER_PATH} push ${DOCKER_IMAGE}"
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Run Docker container
                    sh "${DOCKER_PATH} run -d -p ${PORT_MAPPING} --name ${CONTAINER_NAME} ${DOCKER_IMAGE}"
                }
            }
        }

        stage('Post-Deployment') {
            steps {
                script {
                    // Add post-deployment steps if needed
                    echo 'Post-deployment steps go here'
                }
            }
        }

        stage('Cleanup') {
            steps {
                script {
                    // Clean up: Stop and remove the Docker container
                    sh "${DOCKER_PATH} stop ${CONTAINER_NAME} || true"
                    sh "${DOCKER_PATH} rm ${CONTAINER_NAME} || true"
                }
            }
        }
    }
}
