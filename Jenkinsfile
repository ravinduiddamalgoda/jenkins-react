pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/ravinduiddamalgoda/jenkins-react.git'
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
                    echo 'Deploying application with Apache HTTPD...'
                    
                    // Define the path to the Apache web server directory
                    def apacheDir = '/var/www/html'

                    // Use password-less sudo (ensure sudoers is configured for Jenkins)
                    sh ''' 
                    sudo yum install -y httpd
                    sudo systemctl start httpd
                    sudo systemctl enable httpd
                    '''
                    
                    // Clean the Apache directory (optional, depending on your use case)
                    // sh "sudo rm -rf ${apacheDir}/*"
                    
                    // Copy the build files to Apache's web directory
                    sh "sudo cp -r build/* ${apacheDir}/"
                    
                    // Set correct permissions for the files
                    sh "sudo chown -R apache:apache ${apacheDir}"
                    
                    // Restart Apache to reflect changes
                    sh "sudo systemctl restart httpd"
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




