pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out the application...'
//                 git branch: 'main',
//                     url: 'https://github.com/Narek97/my-app-front.git'
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