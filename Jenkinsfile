pipeline {
    agent any

    environment {
        DOCKER_HUB_USERNAME = 'hemtamang9'  // Your Docker Hub username
        IMAGE_NAME_SERVER = "${DOCKER_HUB_USERNAME}/demopipeline_mern_server:latest"  // Docker Hub image tag for server
        IMAGE_NAME_CLIENT = "${DOCKER_HUB_USERNAME}/demopipeline_mern_client:latest"  // Docker Hub image tag for client
        STACK_NAME = 'mern-curd-stack'  // Example stack name for Docker Swarm
        DOCKER_HUB_CREDENTIALS = 'Dockerhub-token'  // Docker Hub credentials ID for Jenkins
    }

    stages {
        stage('Deploy to Swarm') {
            steps {
                echo "Deploying ${STACK_NAME} to Docker Swarm"
                
                script {
                    // Authenticate with Docker Hub before deploying
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_HUB_CREDENTIALS) {
                        // Deploy the app to Docker Swarm using the existing docker-compose-deploy.yml file
                        sh "docker stack deploy -c docker-compose.yml ${STACK_NAME}"
                    }
                }
            }
        }
    }
}
