pipeline {
    agent {
        docker {
            image 'node:16'  // Requirement 1: Use Node 16 Docker image as the build agent
	    args '-Dorg.jenkinsci.plugins.durabletask.BourneShellScript.LAUNCH_DIAGNOSTICS=true'
        }
    }
    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out the code...'
                git url: 'https://github.com/arbinijam/aws-elastic-beanstalk-express-js-sample', branch: 'main'
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies with npm install --save...'  // Requirement 2: Install dependencies with --save flag
                sh 'npm install --save'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running Snyk security scan...'
                // Install Snyk globally
                sh 'npm install -g snyk'
                // Run Snyk scan, halt on critical vulnerabilities
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

