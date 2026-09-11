pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                checkout scm
            }
        }

        stage('Validate') {
            steps {
                echo 'Validating website files...'
                bat 'dir'
            }
        }

        stage('Docker Build') {
            steps {checkout scm
                echo 'Building Docker image...'
                bat 'docker build -t shobhit-anchor-website .'
            }
        }

        stage('Docker Deploy') {
            steps {
                echo 'Deploying Docker container...'

                bat '''
                docker stop shobhit-anchor || exit 0
                docker rm shobhit-anchor || exit 0
                docker run -d -p 8081:80 --name shobhit-anchor shobhit-anchor-website
                '''
            }
        }
    }

    post {
        success {
            echo 'CI/CD Pipeline completed successfully!'
        }

        failure {
            echo 'CI/CD Pipeline failed!'
        }
    }
}