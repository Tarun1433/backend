pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                script {
                    dir('/opt/backend') {
                        checkout scm
                    }
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    dir('/opt/backend') {
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
