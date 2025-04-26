pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out the application...'
                git branch: 'main',
                    url: 'https://github.com/Narek97/my-app-front.git'
            }
        }

        stage('Lint') {
            agent {
                docker {
                    image 'node:20-alpine'
                    reuseNode true
                }
            }
            steps {
                echo 'Checking code style (lint)...'
                sh 'yarn install'
                sh 'yarn lint'
            }
        }

        stage('Test') {
            agent {
                docker {
                    image 'node:20-alpine'
                    reuseNode true
                }
            }
            steps {
                echo 'Running tests...'
                sh 'yarn install'
                sh 'yarn test'
            }
        }

        stage('Build') {
            agent {
                docker {
                    image 'node:20-alpine'
                    reuseNode true
                }
            }
            steps {
                echo 'Building the application inside Docker...'
                sh 'yarn install'
                sh 'yarn build'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application to S3...'
//                 sh 'aws s3 sync build/ s3://your-bucket-name --delete'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            echo '✅ Pipeline succeeded.'
        }
        failure {
            echo '❌ Pipeline failed.'
        }
    }
}