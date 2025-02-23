pipeline {
    agent any 

    stages {
        stage('Clean Workspace') {
           steps {
                script {
                    cleanWs() // Fixed typo
                }
           }
        }

        stage('Checkout code') {
            steps {
                script {
                    echo 'Checking out code'
                    checkout scm  // Assumes Jenkins is configured with Git SCM
                }
            }
        }

        stage('Show Files and Directories before setup') {
            steps {
                script {
                    echo 'Showing Files and Directories before setup'
                    sh 'ls -la'
                }
            }
        }

        stages {
        stage('Setup Node.js') {
            agent {
                docker {
                    image 'node:22.11.0-alpine3.20' 
                    args '-u root'
                }
            }
            steps {
                script {
                    echo 'Verifying Node.js and npm versions'
                    sh '''
                        node --version
                        npm --version
                    '''
                }
            }
        }
    }


        stage('Install dependencies') {
            steps {
                script {
                    echo 'Installing dependencies'
                    sh 'npm install'
                }
            }
        }

        stage('Show Files and Directories after setup') {
            steps {
                script {
                    echo 'Showing Files and Directories after setup'
                    sh 'ls -la'
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    echo 'Building App'
                    sh 'npm run build'
                }
            }
        }

        stage('Show Files and Directories after build') {
            steps {
                script {
                    echo 'Showing Files and Directories after build'
                    sh 'ls -la'
                }
            }
        }
    }

    post {
        success {
            echo 'Build Completed Successfully '
        }
        failure {
            echo 'Build Failed '
        }
    }
}
