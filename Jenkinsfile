pipeline {
    agent any
    stages {
        stage('Copy and Read File') {
            steps {
                script {
                    // Step 1: Copy the file to the workspace
                    sh 'cp /Users/narekbabayan/Desktop/devops/nest-next-deployment/.env_front .'

                    // Step 2: Read the file from the workspace
                    def fileContent = readFile '.env_front'
                    echo "File Content: ${fileContent}"
                }
            }
        }
    }
}