pipeline {
    agent any

    environment {
        DOCKER_HUB_USERNAME = 'hemtamang9'  
        IMAGE_NAME_SERVER = "${DOCKER_HUB_USERNAME}/mern-curd_server:latest"  
        IMAGE_NAME_CLIENT = "${DOCKER_HUB_USERNAME}/mern-curd_client:latest"  
        STACK_NAME = 'mern-curd-stack'
        DOCKER_HUB_CREDENTIALS = 'Dockerhub-token' 
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the images locally using docker-compose'
               
                sh 'docker-compose -f docker-compose.yaml build'  
            }
        }
        
        stage('Tag and Push to Docker Hub') {
            steps {
                echo 'Tagging and pushing images to Docker Hub'
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_HUB_CREDENTIALS) {
                      
                        // sh "docker tag mern-curd_server:latest ${IMAGE_NAME_SERVER}"
                        sh "docker push ${IMAGE_NAME_SERVER}"

                      
                        // sh "docker tag mern-curd_client:latest ${IMAGE_NAME_CLIENT}"
                        sh "docker push ${IMAGE_NAME_CLIENT}"
                    }
                }
            }
        }

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
