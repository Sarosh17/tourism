pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Build Docker Image') {
            steps {
                bat 'docker build -t tourism-website:test .'
            }
        }
        
        stage('Tag Docker Image') {
            steps {
                bat 'docker tag tourism-website:test sarosh17/tourism-website:test'
            }
        }
        
        stage('Push to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'docker-hub-credential', variable: 'DOCKER_PWD')]) {
                    bat 'docker login -u sarosh17 -p %Sak@1234%'
                    bat 'docker push sarosh17/tourism-website:test'
                }
            }
        }
        
        stage('Deploy Container') {
            steps {
                bat 'docker stop tourism-test-container || true'
                bat 'docker rm tourism-test-container || true' 
                bat 'docker run -d -p 8081:80 --name tourism-test-container sarosh17/tourism-website:test'
            }
        }
    }
    
    post {
        always {
            bat 'docker logout'
        }
    }
}