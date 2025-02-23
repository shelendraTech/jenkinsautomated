pipeline {
    

    stages {

        stage('Clean Workspace') {
            steps {
                script {
                    cleanWs()
                }
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

        stage('Show Files and Directories Before Setup') {
            steps {
                script {
                    echo 'Listing files before setup'
                    sh 'ls -la'
                }
            }
        }

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

        stage('Install Dependencies') {
            steps {
                script {
                    echo 'Installing dependencies'
                    sh 'npm install'
                }
            }
        }

        stage('Show Files and Directories After Setup') {
            steps {
                script {
                    echo 'Listing files after setup'
                    sh 'ls -la'
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    echo 'Building React App'
                    sh 'npm run build'
                }
            }
        }

        stage('Show Files and Directories After Build') {
            steps {
                script {
                    echo 'Listing files after build'
                    sh 'ls -la'
                }
            }
        }
    }


    post {
        success {
            echo 'Build completed successfully'
        }

        failure {
            echo 'Build failed'
        }
    }
}
