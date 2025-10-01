pipeline {
    agent any 

    environment {
        username = "shanze"
        serverip = "192.168.56.105"
        deploydir = "/var/www/html"
    }

    stages {
        stage('Deploy') {
            steps {
                echo "Deploying files to Apache web server..."
                sh '''
                  # Sync app directory content to /var/www/html on server
                  rsync -av --delete ${WORKSPACE}/app/ ${username}@${serverip}:${deploydir}/ --exclude Jenkinsfile --exclude .git

                  # Verify deployed files
                  ssh ${username}@${serverip} "ls -l ${deploydir}/"

                  # Restart Apache server (passwordless sudo already set for shanze)
                  ssh ${username}@${serverip} "sudo systemctl restart apache2"
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Deployment successful! Open http://${serverip}/ in your browser to see changes."
        }
        failure {
            echo "❌ Deployment failed!"
        }
    }
}

