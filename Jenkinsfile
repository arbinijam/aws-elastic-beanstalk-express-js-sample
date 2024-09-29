pipeline {
    agent {
        docker {
            image 'node:16'
        }
    }
    stages {
        stage('Clone Repository') {
            steps {
                // Use checkout scm if you have already configured the repository in Jenkins job
                checkout scm
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
