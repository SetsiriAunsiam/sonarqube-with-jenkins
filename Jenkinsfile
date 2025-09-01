pipeline {
    agent any

 tools {
        nodejs 'NodeJS'  // <-- Use the exact name from Global Tool Configuration
    }


    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/SetsiriAunsiam/sonarqube-with-jenkins.git'
            }
        }

        stage('Build') {
            steps {
                sh 'npm install'
            }
        }

        stage('SonarQube Scan') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh 'npx sonar-scanner -Dsonar.projectKey=sonarqube-with-jenkins'
                }
            }
        }

        stage('Quality Gate') {
            steps {
                timeout(time: 1, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
