pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                script {
                    // Clean up the backend directory if it exists
                    if (fileExists('backend')) {
                        deleteDir()
                    }
                    // Clone the repository into a directory within the workspace
                    dir('backend') {
                        git url: 'https://github.com/Tarun1433/backend.git', branch: 'main'
                    }
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    // Change to the backend directory and run the build
                    dir('backend') {
                        sh 'gradle build'
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'Build finished!'
        }
    }
}
