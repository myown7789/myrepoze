pipeline {
    agent any 

    environment {
        username = "shanze"
        serverip = "192.168.56.105"
        deploydir = "/var/www/html/testsite"
    }

    stages {
        stage('Deploy') {
            steps {
                echo "Deploying files to Apache web server..."
                sh '''
                  # Sync app directory to /var/www/html on server
                  rsync -av --delete  --exclude Jenkinsfile --exclude ".git/" ${WORKSPACE}/ ${username}@${serverip}:${deploydir}/

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

