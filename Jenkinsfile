pipeline {
    agent {
        docker {
            image 'node:22.11.0-alpine3.20'
            args '--user root'
        }
    }

    stages {
        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }

        stage('Checkout Code') {
            steps {
                script {
                    echo 'Checking out code'
                    checkout scm
                }
            }
        }

        stage('Show Files Before Setup') {
            steps {
                echo 'Listing files before setup'
                sh 'ls -la'
            }
        }

        stage('Verify Node.js & npm') {
            steps {
                echo 'Checking Node.js & npm versions'
                sh '''
                    node --version
                    npm --version
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies'
                sh 'npm install'
            }
        }

        stage('Show Files After Setup') {
            steps {
                echo 'Listing files after setup'
                sh 'ls -la'
            }
        }

        stage('Build') {
            steps {
                echo 'Building React App'
                sh 'npm run build'
            }
        }

        stage('Show Files After Build') {
            steps {
                echo 'Listing files after build'
                sh 'ls -la'
            }
        }
    }

    post {
        success {
            echo 'Build completed successfully!'
        }

        failure {
            echo 'Build failed! Please check logs for errors.'
        }
    }
}
