pipeline {
    agent {
        docker {
            image 'node:16'
            args '--privileged -v /var/run/docker.sock:/var/run/docker.sock'
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
                sh 'npm install -g snyk'
                sh 'snyk test --severity-threshold=high'
            }
        }
        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deployment step'
            }
        }
    }
}
