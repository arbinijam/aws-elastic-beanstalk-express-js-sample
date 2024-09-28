pipeline {
    agent {
        docker {
            image 'node:16'  # Use Node.js 16 Docker image as the build agent
            args '--privileged -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/arbinijam/aws-elastic-beanstalk-express-js-sample', branch: 'main'  # Checkout code
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install --save'  # Install Node.js dependencies
            }
        }
        stage('Security Scan') {
            steps {
                sh 'npm install -g snyk'  # Install Snyk for security scanning
                sh 'snyk test --severity-threshold=high'  # Run security scan with Snyk
            }
        }
        stage('Build') {
            steps {
                sh 'npm run build'  # Build the application
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying application...'  # Placeholder for deployment
            }
        }
    }
    post {
        always {
            echo 'Pipeline completed.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
