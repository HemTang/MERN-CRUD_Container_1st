pipeline {
    agent any

    environment {
        DOCKER_HUB_USERNAME = 'hemtamang9'
        IMAGE_NAME_SERVER = "${DOCKER_HUB_USERNAME}/demopipeline_mern_server:latest" 
        IMAGE_NAME_CLIENT = "${DOCKER_HUB_USERNAME}/demopipeline_mern_client:latest"  
        STACK_NAME = 'mern-curd-stack'  
        DOCKER_HUB_CREDENTIALS = 'Dockerhub-token'  
    }

    stages {
        stage('Deploy to Swarm') {
            steps {
                echo "Deploying ${STACK_NAME} to Docker Swarm"
                
                script {
                    
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_HUB_CREDENTIALS) {
                        
                        sh "docker stack deploy -c docker-compose.yaml ${STACK_NAME}"
                    }
                }
            }
        }
    }
}
