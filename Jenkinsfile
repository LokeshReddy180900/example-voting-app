pipeline {
    agent any

    environment {
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk-amd64'
        PATH = "${env.JAVA_HOME}/bin:${env.PATH}"
        DOCKER_CREDENTIALS_ID = 'docker-cred'
       // SONARQUBE_INSTALLATION_NAME = 'Sonarqube'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/LokeshReddy180900/example-voting-app.git'
            }
        }

       

        /*stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv("${SONARQUBE_INSTALLATION_NAME}") {
                    sh 'sonar-scanner'
                }
            }
        } */

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
