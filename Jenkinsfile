pipeline {
    agent any
    environment {
        registry = "ibrahim3/mypythonapp"
        registryCredential = "DockerHub"
    }
    stages {
        stage('Checkout') {
            steps {
                // Checkout code from Git repository
                git credentialsId: 'GitHub', url: 'https://github.com/IBRAHIMCH3/docker-jenkins-integration-sample.git'
            }
        }
        stage('Build') {
            steps {
                // Build Maven project
                sh 'mvn clean package'
            }
        }
        stage('Build Docker Image') {
            steps {
                // Build Docker image
                script {
                    dockerImage = docker.build("${registry}:${BUILD_NUMBER}")
                }
            }
        }
        stage('Upload Image') {
            steps {
                // Push Docker image to Docker registry
                script {
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}
