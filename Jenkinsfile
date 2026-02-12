pipeline {
    agent any

    stages {

        stage('Clone Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/amit6264/Java-springboot-project.git'
            }
        }

        stage('Build Docker Images') {
            steps {
                sh '''
                    docker build -t backend:latest ./backend
                    docker build -t frontend:latest ./frontend
                '''
            }
        }

        stage('Run Containers') {
            steps {
                sh '''
                    # Stop old containers if running
                    docker stop backend || true
                    docker rm backend || true

                    docker stop frontend || true
                    docker rm frontend || true

                    # Run new containers
                    docker run -d --name backend -p 8084:8084 backend:latest
                    docker run -d --name frontend -p 8501:8501 frontend:latest
                '''
            }
        }
    }

    post {
        success {
            echo "🎉 Simple pipeline done!"
        }
        failure {
            echo "❌ Pipeline failed!"
        }
    }
}
