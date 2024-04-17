pipeline {
    agent any
    
    environment {
        DOCKER_IMAGE_NAME = "my-docker-image"
        GIT_REPO_URL = "https://github.com/your-username/your-repo.git"
        DOCKERFILE_PATH = "./Dockerfile"
    }
    
    stages {
        stage('Clone Repository') {
            steps {
                script {
                    // Clone the Git repository
                    git branch: 'master', url: GIT_REPO_URL
                }
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    docker.build(DOCKER_IMAGE_NAME, "-f ${DOCKERFILE_PATH} .")
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    // Push the Docker image to a Docker registry
                    docker.withRegistry('https://registry.example.com', 'docker-registry-credentials') {
                        docker.image(DOCKER_IMAGE_NAME).push('latest')
                    }
                }
            }
        }
    }
