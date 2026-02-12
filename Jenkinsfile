pipeline {
    agent any

    stages {
        
        stage('Clone Repo') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/amit6264/YOUR_REPO.git'
            }
        }

        stage('Build Backend Jar') {
            steps {
                dir('backend') {
                    sh 'mvn clean package -DskipTests'
                }
            }
        }

        stage('Build Backend Docker Image') {
            steps {
                dir('backend') {
                    sh 'docker build -t backend:latest .'
                }
            }
        }

        stage('Build Frontend Docker Image') {
            steps {
                dir('frontend') {
                    sh 'docker build -t frontend:latest .'
                }
            }
        }

        stage('Stop Existing Containers') {
            steps {
                sh '''
                    docker stop backend || true
                    docker rm backend || true

                    docker stop frontend || true
                    docker rm frontend || true
                '''
            }
        }

        stage('Run Backend Container') {
            steps {
                sh 'docker run -d --name backend -p 8084:8084 backend:latest'
            }
        }

        stage('Run Frontend Container') {
            steps {
                sh 'docker run -d --name frontend -p 8501:8501 frontend:latest'
            }
        }
    }

    post {
        success {
            echo "Deployment Successful!"
        }
        failure {
            echo "Deployment Failed!"
        }
    }
}
