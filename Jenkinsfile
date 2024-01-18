pipeline {
    agent any

    environment {
        IMAGE_NAME = 'myimage'
        CONTAINER_NAME = 'my-container321'
        PORT_MAPPING = '8084:5901'
    }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image
                    docker.build(env.IMAGE_NAME, '.')
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Run Docker container
                    def container = docker.image(env.IMAGE_NAME).run("-p ${env.PORT_MAPPING} --name ${env.CONTAINER_NAME} -d")
                    // Retrieve the container ID for further use if needed
                    def containerId = container.id
                    echo "Docker container ID: ${containerId}"
                }
            }
        }

        stage('Post-Deployment') {
            steps {
                script {
                    // Perform post-deployment tasks if needed
                    echo 'Post-deployment tasks...'
                    // Example: Wait for the container to start (adjust as needed)
                    sh "sleep 30"
                    // Example: Print container logs
                    sh "docker logs ${env.CONTAINER_NAME}"
                }
            }
        }

        stage('Cleanup') {
            steps {
                script {
                    // Clean up: Stop and remove the Docker container
                    sh "docker stop ${env.CONTAINER_NAME} || true"
                    sh "docker rm ${env.CONTAINER_NAME} || true"
                }
            }
        }
    }
}
