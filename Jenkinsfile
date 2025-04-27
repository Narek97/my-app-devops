pipeline {
    agent any
    stages {
        stage('Check rnv.file') {
            steps {
                script {
                    // Check if the file exists
                    if (fileExists('./home/front/rnv.file')) {
                        echo 'rnv.file exists'
                        // Optionally, you can add commands to read or process the file
                        // For example, to display the file content:
                        sh 'cat ./home/front/rnv.file'
                    } else {
                        error 'rnv.file does not exist'
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
            echo 'Pipeline failed due to missing rnv.file'
        }
    }
}