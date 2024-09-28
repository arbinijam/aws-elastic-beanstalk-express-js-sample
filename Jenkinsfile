pipeline {
    agent {
        docker {
            image 'node:16'
            args '--privileged -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    stages {
        stage('Install Docker') {
            steps {
                sh '''
                apt-get update && \
                apt-get install -y apt-transport-https ca-certificates curl gnupg2 software-properties-common && \
                curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - && \
                add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable" && \
                apt-get update && \
                apt-get install -y docker-ce-cli
                '''
            }
        }
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
