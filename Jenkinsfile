pipeline {
    agent any
    stages {

        stage('Checkout Backend') {
            steps {
                dir('backend') {
                    echo 'Checking out the backend application...'
                    git branch: 'main',
                        url: 'https://github.com/Narek97/my-app-back.git'
                }
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
                dir('backend') {
                    echo 'Checking backend code style (lint)...'
                    sh 'yarn install'
                    sh 'yarn lint'
                }
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
                dir('backend') {
                    echo 'Running backend tests...'
                    sh 'yarn install'
                    sh 'yarn test'
                }
            }
        }

        stage('Deploy Backend') {
            steps {
                dir('backend') {
                    echo 'Deploying backend application to S3...'
                    // Example:
                    // sh 'aws s3 sync build/ s3://your-back-bucket-name --delete'
                }
            }
        }

        stage('Checkout Frontend') {
            steps {
                dir('frontend') {
                    echo 'Checking out the frontend application...'
                    git branch: 'main',
                        url: 'https://github.com/Narek97/my-app-front.git'
                }
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
                dir('frontend') {
                    echo 'Checking frontend code style (lint)...'
                    sh 'yarn install'
                    sh 'yarn lint'
                }
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
                dir('frontend') {
                    echo 'Running frontend tests...'
                    sh 'yarn install'
                    sh 'yarn test'
                }
            }
        }

//         stage('Build Frontend') {
//             agent {
//                 docker {
//                     image 'node:20-alpine'
//                     reuseNode true
//                 }
//             }
//             steps {
//                 dir('frontend') {
//                     echo 'Building the frontend application inside Docker...'
//                     sh 'yarn install'
//                     sh 'yarn build'
//                 }
//             }
//         }
        stage('Build Frontend') {
            agent {
                docker {
                    image 'node:20-alpine'
                    reuseNode true
                }
            }
            steps {
                dir('frontend') {
                    echo 'Building the frontend application inside Docker...'
                    sh 'docker compose -f docker-compose-build.yml --env-file ./home/front/.env_front build'
                }
            }
        }

        stage('Deploy Frontend') {
            steps {
                dir('frontend') {
                    echo 'Deploying frontend application to S3...'
                    // Example:
                    // sh 'aws s3 sync build/ s3://your-front-bucket-name --delete'
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
