pipeline {
    agent any

    stages {

        stage('Read File') {
           steps {
                script {
                    def fileContent = readFile '/Users/narekbabayan/Desktop/devops/nest-next-deployment/.env_front'
                    echo "File Content: ${fileContent}"
                }
           }
        }

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

        stage('Build Backend') {
            agent {
                docker {
                    image 'docker:20.10' // Use a Docker image with docker CLI and compose
                    args '--user root -v /var/run/docker.sock:/var/run/docker.sock' // Mount Docker socket
                    reuseNode true
                }
            }
            steps {
                echo 'Building the backend application inside Docker...'
                sh 'yarn install'
                sh 'yarn build'
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
                sh 'yarn install'
                sh 'yarn build'
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