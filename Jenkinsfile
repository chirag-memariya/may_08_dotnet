pipeline {
    agent any
    environment {
        APP_NAME = "my-web-dotnet-app"
        APP_PORT = "5000"
        IMAGE_TAG = "latest"
        DOCKER_REGISTRY = "https://hub.docker.com/u/memariyachirag126"
    }
    stages {
        stage('Build') {
            steps {
                
                // Build the project
                sh 'dotnet build'
            }
        }
        stage('test') {
            steps {
                
                // test the project
                sh 'dotnet test'
            }
        }
        stage('pulbish'){
            steps{
                // Publish the project
                sh 'dotnet publish -c Release -o ./publish'
            }
        }
        stage('Docker Build') {
            steps {
                // Build Docker image
                script {
                    docker.build("${DOCKER_REGISTRY}/${APP_NAME}:${IMAGE_TAG}", "--build-arg APP_PORT=${APP_PORT} .")
                }
            }
        }
    }
}
