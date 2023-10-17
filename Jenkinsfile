pipeline {
    agent {
        node {
            label 'node-agent'
        }
    }
    environment {
        DOCKER_HUB = credentials('docker-hub')
        VERCEL = credentials('vercel-jenkins')
    }
    triggers {
        pollSCM '*/5 * * * *'
    }
    stages {
        stage('Lint Code') {
            steps {
                sh 'npm run lint'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('mytravels-guide:latest')
                    docker.withRegistry('https://registry.hub.docker.com', DOCKER_HUB) {
                        docker.image('mytravels-guide:latest').push()
                    }
                }
            }
        }
        stage('Deploy to Vercel') {
            steps {
                sh 'vercel login --token $VERCEL'
                sh 'vercel --prod --json > deployment.json'
            }
        }
        stage('Export Deployment URL') {
            steps {
                script {
                    def deploymentData = readJSON file: 'deployment.json'
                    def deploymentURL = deploymentData.url
                    currentBuild.description = "Deployment URL: $deploymentURL"
                    echo "Deployment URL: $deploymentURL"
                }
            }
        }
    }
}