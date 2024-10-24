pipeline {
    agent { label 'built-in' }

    environment {
        DOCKER_USERNAME = 'ingyelkhateeb'
        DOCKER_PASSWORD = '5557070i*'
        IMAGE_NAME = 'devops-project-alx_swd1_m2d:latest'
        CONTAINER_PORT = '9090'
        HOST_PORT = '9090'
        CONTAINER_NAME = 'my_container'
    }

    stages {
        
        stage('Clone Repository') {
            steps {
                git 'https://github.com/ingy-elkhateeb/Nhorizon-DevOps-Task---ALX_SWD1_M2d'
            }
        }
        
        stage('Build Docker Image') {
            
            steps {
                script {
                    sh "docker build -t $DOCKER_USERNAME/$IMAGE_NAME ."
                }
            }
        }
        
        stage('Login to Docker Hub') {
            
            steps {
                script {
                    // Log in to Docker Hub
                    // Log in to Docker Hub
                    sh 'echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin'
                    
                    // Push the image to Docker Hub
                    sh "docker push $DOCKER_USERNAME/$IMAGE_NAME"
                        }
            }
        }
        
        stage('Pull Docker Image') {
            steps {
                script {
                    // Log in to Docker Hub
                    sh 'echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin'
                    
                    // Pull the pre-built image from Docker Hub
                    sh "docker pull $DOCKER_USERNAME/$IMAGE_NAME"
                }
            }
        }

        stage('Cleanup Existing Container') {
            steps {
                script {
                    // Stop and remove the existing container if it exists
                    sh """
                    if [ \$(docker ps -aq -f name=$CONTAINER_NAME) ]; then
                        docker stop $CONTAINER_NAME || true
                        docker rm $CONTAINER_NAME || true
                    fi
                    """
                }
            }
        }

        stage('Run Docker Image') {
            steps {
                script {
                    // Run the Docker container and expose the required port (80)
                    sh "docker run --name $CONTAINER_NAME -d -p $HOST_PORT:$CONTAINER_PORT $DOCKER_USERNAME/$IMAGE_NAME"
                }
            }
        }

        stage('Verify Container') {
            steps {
                script {
                    // Check if the container is running
                    sh "docker ps"
                }
            }
        }
    }
}
