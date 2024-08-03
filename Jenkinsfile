
pipeline {
    agent any

    environment {
        NODEJS_VERSION = '18'
    }

    tools {
        // Install the NodeJS tool
        nodejs NODEJS_VERSION
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the source code from your repository
                git 'https://github.com/rolniuq/nestjs-nats'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Install project dependencies
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                // Build the project
                sh 'npm run build'
            }
        }

        stage('Test') {
            steps {
                // Run the tests
                sh 'npm run test'
            }
        }

        stage('Lint') {
            steps {
                // Lint the code
                sh 'npm run lint'
            }
        }
    }

    post {
        always {
            // Archive test results and other artifacts if necessary
            junit '**/test-results.xml'
            archiveArtifacts artifacts: '**/dist/**', allowEmptyArchive: true
        }
        success {
            // Actions to perform on success
            echo 'Build and tests succeeded!'
        }
        failure {
            // Actions to perform on failure
            echo 'Build or tests failed.'
        }
    }
}

