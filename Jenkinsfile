pipeline {
    agent {
        docker {
            image 'node:16'
        }
    }
    stages {
        stage('Clone Repository') {
            steps {
                script {
                    // Clone your repository manually if needed
                    sh 'git clone https://github.com/arbinijam/aws-elastic-beanstalk-express-js-sample.git .'
                }
            }
        }
        stage('Build') {
            steps {
                script {
                    echo 'Building the project...'
                    sh 'npm install --save'
                }
            }
        }
    }
    post {
        success {
            echo 'Build successful!'
        }
        failure {
            echo 'Build failed.'
        }
    }
}
