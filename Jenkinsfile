pipeline {
    agent any

    stages {

        stage('Clone Code') {
            steps {
                echo "Code Cloned Automatically by Jenkins from SCM"
            }
        }

        stage('Build Docker Images') {
    steps {
        sh '''
        sudo docker-compose -f docker-compose.yml build
        '''
               }
             }

        stage('Stop Old Containers') {
            steps {
                sh '''
                    docker-compose -f docker-compose.yml down
                '''
            }
        }

        stage('Start New Containers') {
            steps {
                sh '''
                    docker-compose -f docker-compose.yml up -d
                '''
            }
        }
    }
}
