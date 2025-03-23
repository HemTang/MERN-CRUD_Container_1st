pipeline {
    agent any

    environment {
        DOCKER_HUB_USERNAME = 'hemtamang9'  // Your Docker Hub username
        IMAGE_NAME_SERVER = "${DOCKER_HUB_USERNAME}/demopipeline_mern_server:latest"  // Image tag for server
        IMAGE_NAME_CLIENT = "${DOCKER_HUB_USERNAME}/demopipeline_mern_client:latest"  // Image tag for client
        DOCKER_HUB_CREDENTIALS = 'dockerhub-token'  // Jenkins credentials ID for Docker Hub
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the images locally using docker-compose'
                sh 'docker-compose -f docker-compose-build.yml build'  // Build the images for both server and client
            }
        }
        stage('Tag and Push to Docker Hub') {
            steps {
                echo 'Tagging and pushing images to Docker Hub'
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_HUB_CREDENTIALS) {
                        // Tag and push the server image
                        sh "docker tag demopipeline_mern_server:latest ${IMAGE_NAME_SERVER}"  // Tag the server image
                        sh "docker push ${IMAGE_NAME_SERVER}"  // Push the server image to Docker Hub

                        // Tag and push the client image
                        sh "docker tag demopipeline_mern_client:latest ${IMAGE_NAME_CLIENT}"  // Tag the client image
                        sh "docker push ${IMAGE_NAME_CLIENT}"  // Push the client image to Docker Hub
                    }
                }
            }
        }
    }
}
