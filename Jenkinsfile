pipeline {
    agent { label 'test' }

    stages {
        stage('Setup') {
            steps {
                script {
                    // Switch to root user
                    sh "sudo su"
                }
            }
        }
        stage('Clear Workspace') {
            steps {
                sh "rm -rf /opt/backend/*"
            }
        }
        stage('Clone Repository') {
            steps {
                dir('/opt/backend') {
                    sh "git clone https://github.com/Tarun1433/backend.git"
                }
            }
        }
        stage('Build') {
            steps {
                dir('/opt/backend/workspace/Gradle_remote_build') {
                    sh "gradle build"
                }
            }
        }
        stage('Deployment') {
            steps {
                dir('/opt/backend/workspace/Gradle_remote_build/my-webapp/build/libs') {
                    sh "mv my-webapp-0.0.1-SNAPSHOT.jar app.jar"
                    sh "cp app.jar /var"
                }
            }
        }
    }
}
