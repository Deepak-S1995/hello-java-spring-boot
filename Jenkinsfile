pipeline {
    agent any
    
    environment {
        DOCKER_IMAGE_NAME = "my-docker-image"
        GIT_REPO_URL = "https://github.com/Deepak-S1995/hello-java-spring-boot.git"
        DOCKERFILE_PATH = "./Dockerfile"
        OPENJDK_VERSION = "11"
        MAVEN_HOME = tool 'Maven'
    }
    
    stages {
        stage('Clone Repository') {
            steps {
                script {
                    git branch: 'master', url: GIT_REPO_URL
                }
            }
        }
        
        stage('Build Application') {
            steps {
                script {
                    sh "${MAVEN_HOME}/bin/mvn clean install"
                }
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE_NAME}:${OPENJDK_VERSION}", "-f ${DOCKERFILE_PATH} --build-arg OPENJDK_VERSION=${OPENJDK_VERSION} .")
                }
            }
        }
    }
}
