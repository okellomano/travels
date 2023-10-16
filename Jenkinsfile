pipeline {
    agent {
        node {
            label 'docker-agent-alpine'
        }
    }
    triggers {
        pollSCM '*/5 * * * *'
    }
    stages {
        stage('Build') {
            steps {
                echo "Building..."
                sh '''
                echo "Build job here"
                '''
            }
        }
        stage('Test') {
            steps {
                echo "Testing..."
            }
        }
        stage('Deliver') {
            steps {
                echo "Devliver..."
            }
        }
    }
}