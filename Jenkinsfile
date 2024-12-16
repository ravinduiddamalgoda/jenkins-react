pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/chathurajayasank/contact-us-bmc-car.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                script {
                    sh 'npm install'
                }
            }
        }
        stage('Build Application') {
            steps {
                script {
                    sh 'npm run build'
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    echo 'Deploying application...'
                    // Define deployment directory
                    def deploymentDir = '/var/www/contact-us-bmc-car'

                    // Copy build files to the deployment directory
                    sh "cp -r build/* ${deploymentDir}"

                }
            }
        }
    }
    post {
        always {
            echo 'Pipeline execution complete.'
        }
        success {
            echo 'Deployment succeeded.'
        }
        failure {
            echo 'Deployment failed. Check logs for details.'
        }
    }
}
