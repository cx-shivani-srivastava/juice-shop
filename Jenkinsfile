/* Requires the Docker Pipeline plugin */
pipeline {
    agent { docker { image 'node:24.15.0-alpine3.23' } }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/cx-shivani-srivastava/juice-shop.git', branch: 'master'
            }
        }

        stage('Build') {
            steps {
                echo 'Installing dependencies...'
                sh 'node --version'
                sh 'npm --version'
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'npm test'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                sh 'npm start'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed! Check the logs above.'
        }
        always {
            echo 'Pipeline execution finished.'
        }
    }
}
