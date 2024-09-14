pipeline {
    agent {
        docker {
            image 'node:16'
            label 'docker'
        }
    }
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/arbinijam/aws-elastic-beanstalk-express-js-sample', branch: 'main'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install --save'
            }
        }

        stage('Security Scan') {
            steps {
                // Install Snyk and run security scan
                sh 'npm install -g snyk'
                sh 'snyk test'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test'
            }
        }

        stage('Build') {
            steps {
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
        failure {
            echo 'Pipeline failed.'
        }
    }
}

