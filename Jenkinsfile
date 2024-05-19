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
        stage('Build') {
            steps {
                dir('/opt/backend/workspace') {
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
