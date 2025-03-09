pipeline {
    agent any
    
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'test', url: 'https://github.com/Sarosh17/tourism.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t tourism-website-test .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run -d -p 4080:80 tourism-website-test'
            }
        }
    }
}
