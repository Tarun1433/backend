pipeline {
    agent { label 'test' }
    
    parameters {
        string(name: 'staging_server', defaultValue: '13.232.37.20', description: 'Remote Staging Server')
    }

    stages {
        stage('Prepare Environment') {
            steps {
                script {
                    echo "Changing directory to /project/backend"
                    dir('/project/backend') {
                        echo "Cleaning up the directory"
                        sh 'rm -fr backend'
                        echo "Cloning the repository..."
                        sh 'git clone https://github.com/Tarun1433/backend.git'
                    }
                }
            }
        }
        
        stage('Build') {
            steps {
                script {
                    echo "Changing directory to the cloned repository"
                    dir('/project/backend/backend') {
                        echo "Executing gradle build task..."
                        sh './gradle build'
                    }
                }
            }
            post {
                success {
                    script {
                        echo "Changing directory to the built application"
                        dir('/project/backend/backend/my-webapp/build/libs') {
                            echo "Renaming the JAR file..."
                            sh 'mv my-webapp-0.0.1-SNAPSHOT.jar app.jar'
                            echo "Copying the JAR file to /var/www/backend/"
                            sh 'cp app.jar /var/www/backend/'
                        }
                    }
                }
            }
        }
        
        stage ('Deploy to Staging') {
            steps {
                script {
                    echo "Deploying to Staging Server..."
                    sh "scp -v -o StrictHostKeyChecking=no /var/www/backend/app.jar root@${params.staging_server}:/opt/tomcat/webapps/"
                }
            }
        }
    }
}
