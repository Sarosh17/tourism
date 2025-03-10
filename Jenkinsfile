pipeline {
    agent any
    
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'test', url: 'https://github.com/Sarosh17/tourism.git'
            }
        }

        stage('Clean Old Containers & Images') {
            steps {
                script {
                    sh 'docker stop tourism-test || true && docker rm tourism-test || true'
                    sh 'docker rmi tourism-website-test || true'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t tourism-website-test .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run -d -p 4080:80 --name tourism-test tourism-website-test'
            }
        }
    }
}
