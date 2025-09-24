pipeline {
    agent any 

    environment {
        username = "shanze"
        serverip = "192.168.56.105"
        deploydir = "/var/www/html/app"
    }

    stages {
        stage('Deploy') {
            steps {
                echo "Deploying files to Apache web server..."
                sh '''
                  # Sync all files from workspace to server
                  rsync -av ${WORKSPACE}/* ${username}@${serverip}:/var/www/html/ --exclude Jenkinsfile --exclude .git

                  # Delete files from app directory
                  ssh ${username}@${serverip} "rm -f ${deploydir}/file1.html ${deploydir}/file2.html"

                  # Verify modified files exist after deployment
                  ssh ${username}@${serverip} "ls -l ${deploydir}/file3.html ${deploydir}/file4.html ${deploydir}/file5.html"

                  # Restart Apache server
                  sudo systemctl restart apache2
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Deployment successful! Open http://${serverip}/app/ in your browser to see changes."
        }
        failure {
            echo "❌ Deployment failed!"
        }
    }
}

