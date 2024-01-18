pipeline {
    agent any

    environment {
        DOCKERFILE_PATH = './Dockerfile'  // Specify the path to your Dockerfile
        IMAGE_NAME = 'myimage'
        CONTAINER_NAME = 'mycontainer'
        PORT_MAPPING = '8080:80'  // Adjust the port mapping as needed
    }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image
                    docker.build(env.IMAGE_NAME, "-f ${env.DOCKERFILE_PATH} .")
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Run Docker container
                    docker.image(env.IMAGE_NAME).withRun("-p ${env.PORT_MAPPING} --name ${env.CONTAINER_NAME}")
                }
            }
        }

        stage('Cleanup') {
            steps {
                script {
                    // Clean up: Stop and remove the Docker container
                    docker.container(env.CONTAINER_NAME).stop()
                    docker.container(env.CONTAINER_NAME).remove(force: true)
                }
            }
        }
    }
}
