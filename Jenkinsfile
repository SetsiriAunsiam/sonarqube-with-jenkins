pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                git 'https://github.com/SetsiriAunsiam/sonarqube-with-jenkins.git'
                bat "npm install"
            }
        }

        stage('Scan') {
            steps {
                withSonarQubeEnv(installationName: 'sq1') {
                    bat "npm install sonar-scanner"
                    bat 'npx sonar-scanner -X -X -Dsonar.projectKey=mywebapp'
                }
            }
        }
    }
}