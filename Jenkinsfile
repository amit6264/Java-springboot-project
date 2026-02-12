pipeline {
    agent any

    environment {
        BACKEND_IMAGE = "backend:latest"
        FRONTEND_IMAGE = "frontend:latest"
    }

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/amit6264/Java-springboot-project.git'
            }
        }

        stage('Build Backend JAR') {
            steps {
                dir('backend') {
                    sh 'mvn clean package -DskipTests'
                }
            }
        }

        stage('Build Backend Docker Image') {
            steps {
                dir('backend') {
                    sh 'docker build -t ${BACKEND_IMAGE} .'
                }
            }
        }

        stage('Build Frontend Docker Image') {
            steps {
                dir('frontend') {
                    sh 'docker build -t ${FRONTEND_IMAGE} .'
                }
            }
        }

        stage('Stop Old Containers') {
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
                sh '''
                    docker run -d --name backend -p 8084:8084 ${BACKEND_IMAGE}
                '''
            }
        }

        stage('Run Frontend Container') {
            steps {
                sh '''
                    docker run -d --name frontend -p 8501:8501 ${FRONTEND_IMAGE}
                '''
            }
        }
    }

    post {
        success {
            echo "🚀 Deployment completed successfully!"
        }
        failure {
            echo "❌ Deployment failed!"
        }
    }
}
