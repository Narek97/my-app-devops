pipeline {
    agent any
    stages {

        stage('Checkout Backend') {
            steps {
                echo 'Checking out the backend application...'
                git branch: 'main',
                    url: 'https://github.com/Narek97/my-app-back.git'
            }
        }

        stage('Lint Backend') {
            agent {
                docker {
                    image 'node:20-alpine'
                    reuseNode true
                }
            }
            steps {
                echo 'Checking backend code style (lint)...'
                sh 'yarn install'
                sh 'yarn lint'
            }
        }

        stage('Test Backend') {
            agent {
                docker {
                    image 'node:20-alpine'
                    reuseNode true
                }
            }
            steps {
                echo 'Running backend tests...'
                sh 'yarn install'
                sh 'yarn test'
            }
        }

        stage('Deploy Backend') {
            steps {
                echo 'Deploying backend application to S3...'
                // sh 'aws s3 sync build/ s3://your-back-bucket-name --delete'
            }
        }

        // Frontend stages (unchanged, included for completeness)
        stage('Checkout Frontend') {
            steps {
                echo 'Checking out the frontend application...'
                git branch: 'main',
                    url: 'https://github.com/Narek97/my-app-front.git'
            }
        }

        stage('Lint Frontend') {
            agent {
                docker {
                    image 'node:20-alpine'
                    reuseNode true
                }
            }
            steps {
                echo 'Checking frontend code style (lint)...'
                sh 'yarn install'
                sh 'yarn lint'
            }
        }

        stage('Test Frontend') {
            agent {
                docker {
                    image 'node:20-alpine'
                    reuseNode true
                }
            }
            steps {
                echo 'Running frontend tests...'
                sh 'yarn install'
                sh 'yarn test'
            }
        }

        stage('Build Frontend') {
            agent {
                docker {
                    image 'node:20-alpine'
                    reuseNode true
                }
            }
            steps {
                echo 'Building the frontend application inside Docker...'
//                 sh 'yarn install'
//                 sh 'yarn build'
                sh 'ls -la ./home/front/.env_front || echo ".env_front not found"'
            }
        }

        stage('Deploy Frontend') {
            steps {
                echo 'Deploying frontend application to S3...'
                // sh 'aws s3 sync build/ s3://your-front-bucket-name --delete'
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