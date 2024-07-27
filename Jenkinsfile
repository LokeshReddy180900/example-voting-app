pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS_ID = 'docker-cred'
        SONARQUBE_CREDENTIALS_ID = 'sonarqube'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/LokeshReddy180900/example-voting-app.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh 'sonar-scanner'
                }
            }

        }



        stage('Build Docker Images') {
            steps {
                script {
                    docker.build('ambatilokesh/python-vote-app', './vote')
                    docker.build('ambatilokesh/nodejs-results-app', './result')
                    docker.build('ambatilokesh/dotnet-worker', './worker')
                }
            }
        }
        // Other stages follow...
    }
}
