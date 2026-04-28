pipeline {
    agent any

    tools {
        nodejs 'NodeJS-24'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Installing dependencies...'
                bat 'node --version'
                bat 'npm --version'
                bat 'npm install'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                catchError(buildResult: 'UNSTABLE', stageResult: 'UNSTABLE') {
                    bat 'npm test'
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                bat 'echo Deploy step completed successfully'
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline completed successfully!'
        }
        unstable {
            echo '⚠️ Pipeline completed with test warnings - check test results!'
        }
        failure {
            echo '❌ Pipeline failed! Check the logs above.'
        }
        always {
            echo 'Pipeline execution finished.'
        }
    }
}
