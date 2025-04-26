pipeline {
    agent any

    stages {
        stage('Checkout') {
            parallel {
                stage('Checkout Backend') {
                    steps {
                        echo 'Checking out the backend application...'
                        git branch: 'main',
                            url: 'https://github.com/Narek97/my-app-back.git'
                    }
                }
                stage('Checkout Frontend') {
                    steps {
                        echo 'Checking out the frontend application...'
                        git branch: 'main',
                            url: 'https://github.com/Narek97/my-app-front.git'
                    }
                }
            }
        }

        stage('Process Backend') {
            agent {
                docker {
                    image 'node:20-alpine'
                    reuseNode true
                }
            }
            stages {
                stage('Lint Backend') {
                    steps {
                        dir('my-app-back') {
                            echo 'Checking backend code style (lint)...'
                            sh 'yarn install'
                            sh 'yarn lint'
                        }
                    }
                }
                stage('Test Backend') {
                    steps {
                        dir('my-app-back') {
                            echo 'Running backend tests...'
                            sh 'yarn install'
                            sh 'yarn test'
                        }
                    }
                }
                stage('Build Backend') {
                    steps {
                        dir('my-app-back') {
                            echo 'Building the backend application...'
                            sh 'yarn install'
                            sh 'yarn build'
                        }
                    }
                }
            }
        }

        stage('Process Frontend') {
            agent {
                docker {
                    image 'node:20-alpine'
                    reuseNode true
                }
            }
            stages {
                stage('Lint Frontend') {
                    steps {
                        dir('my-app-front') {
                            echo 'Checking frontend code style (lint)...'
                            sh 'yarn install'
                            sh 'yarn lint'
                        }
                    }
                }
                stage('Test Frontend') {
                    steps {
                        dir('my-app-front') {
                            echo 'Running frontend tests...'
                            sh 'yarn install'
                            sh 'yarn test'
                        }
                    }
                }
                stage('Build Frontend') {
                    steps {
                        dir('my-app-front') {
                            echo 'Building the frontend application...'
                            sh 'yarn install'
                            sh 'yarn build'
                        }
                    }
                }
            }
        }


        stage('Deploy') {
            steps {
                echo 'Deploying applications to S3...'
                dir('my-app-back') {
                    echo 'Deploying backend to S3...'
                    // sh 'aws s3 sync build/ s3://your-backend-bucket-name --delete'
                }
                dir('my-app-front') {
                    echo 'Deploying frontend to S3...'
                    // sh 'aws s3 sync build/ s3://your-frontend-bucket-name --delete'
                }
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