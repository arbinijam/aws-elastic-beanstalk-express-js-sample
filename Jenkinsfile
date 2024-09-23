pipeline {
    agent {
        docker {
            image 'node:16'  // Use Node 16 Docker image as the build agent
            args '--privileged -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out the code...'
                git url: 'https://github.com/your-username/aws-elastic-beanstalk-express-js-sample', branch: 'main'
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies with npm install --save...'
                sh 'npm install --save'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running Snyk security scan...'
                sh 'npm install -g snyk'
                sh 'snyk test --severity-threshold=high'
            }
        }

        stage('Test') {
            steps {
                echo 'Running unit tests...'
                sh 'npm test'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the application...'
                sh 'npm run build'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
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
        success {
            echo 'Pipeline completed successfully.'
        }
    }
}

