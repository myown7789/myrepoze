pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Building project..."
            }
        }
        stage('Test') {
            steps {
                echo "Running tests..."
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploying files to Apache web server..."
                sh '''
                  sudo rsync -avz $WORKSPACE/ /var/www/html/ --exclude Jenkinsfile --exclude .git
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
