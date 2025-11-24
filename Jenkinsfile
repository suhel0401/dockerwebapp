pipeline {
    agent any

    environment {
        COMPOSE_FILE = 'docker-compose.yml'
    }

    stages {

        stage('Clone Code') {
            steps {
                echo "Code Cloned Automatically by Jenkins from SCM"
            }
        }

        stage('Build Docker Images') {
            steps {
                echo "Building Docker images..."
                sh """
                    docker-compose -f \$COMPOSE_FILE build
                """
            }
        }

        stage('Stop Old Containers') {
            steps {
                echo "Stopping existing containers if any..."
                sh """
                    docker-compose -f \$COMPOSE_FILE down || true
                """
            }
        }

        stage('Start New Containers') {
            steps {
                echo "Starting containers..."
                sh """
                    docker-compose -f \$COMPOSE_FILE up -d
                """
            }
        }

        stage('List Running Containers') {
            steps {
                echo "Listing all running containers..."
                sh 'docker ps'
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully!"
        }
        failure {
            echo "Pipeline failed. Check logs for details."
        }
    }
}
