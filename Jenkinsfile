pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/WajidAli05/lab11.git'
            }
        }

        stage('Install dependencies') {
            steps {
                script {
                    sh 'npm install'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t wajidali05/lab11 .'
                }
            }
        }

        stage('Run Docker Image') {
            steps {
                script {
                    sh 'docker run -d -p 3000:3000 wajidali05/lab11'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'wajidali05') {
                        docker.image("wajidali05/lab11:latest").push()
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'The pipeline has executed successfully!'
        }
        failure {
            echo 'The pipeline failed.'
        }
    }
}
