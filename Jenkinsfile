pipeline {
    agent { label 'test' }

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
                    dir('backend') {
                        // Ensure gradlew is executable and run the build
                        sh 'chmod +x gradlew'
                        sh './gradlew build'
                    }
                }
            }
        }

        stage('Rename and Deploy') {
            steps {
                script {
                    dir('backend/my-webapp/build/libs') {
                        // Rename the jar file
                        sh 'mv my-webapp-0.0.1-SNAPSHOT.jar app.jar'
                        // Move the jar file to /var directory
                        sh 'mv app.jar /var/'
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
