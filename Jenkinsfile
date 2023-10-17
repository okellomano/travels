pipeline {
    agent {
        node {
            label 'docker-agent-alpine'
        }
    }
    triggers {
        pollSCM '* * * * *'
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
                sh '''
                echo "Perform code coverage, code quality and SCA tests"
                '''
            }
        }
        stage('Deliver') {
            steps {
                echo "Devliver..."
            }
        }
    }
}