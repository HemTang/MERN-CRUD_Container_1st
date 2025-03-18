pipeline{
    agent any

    stages{
        stage("Build"){

            steps{
                echo 'Building the image/container'
                sh 'docker-compose -f docker-compose.yaml build'
               
            }

        }
        stage("Test"){

            steps{
                echo 'Running the test'
                
            }

        }
        stage("Deploy"){

            steps{
                echo 'Deploying to production'
                sh 'docker-compose -f docker-compose.yaml up -d'
               
            }

        }
        
    }
}
