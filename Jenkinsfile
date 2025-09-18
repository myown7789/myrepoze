pipeline {
    agent any
    
        environment {
            username = "shanze"
            serverip = "192.168.56.105"
    }
    stages {
        stage('Deploy') {
            steps {
                echo "Deploying files to Apache web server..."
                sh '''
                  rsync -av ${WORKSPACE}/* ${username}@${serverip}:/var/www/html/ --exclude Jenkinsfile --exclude .git
                  sudo systemctl restart apache2
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Deployment successful! Open your server IP in a browser to see index.html"
        }
        failure {
            echo "❌ Deployment failed!"
        }
    }
}
