pipeline {
    agent any
    stages {
        stage('Check .env_front') {
            steps {
                script {
                    // Check if the file exists
                    if (fileExists('./home/front/.env_front')) {
                        echo '.env_front exists'
                        // Optionally, you can add commands to read or process the file
                        // For example, to display the file content:
                        sh 'cat ./home/front/.env_front'
                    } else {
                        error '.env_front does not exist'
                    }
                }
            }
        }
    }
    post {
        always {
            echo 'Pipeline execution completed'
        }
        failure {
            echo 'Pipeline failed due to missing .env_front'
        }
    }
}