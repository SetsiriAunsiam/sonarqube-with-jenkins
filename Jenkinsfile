pipeline {
    agent any

    environment {
        SONARQUBE = credentials('sonarqube-token') // ชื่อ Credential ของ Jenkins
    }
    tools {
        nodejs 'NodeJS' // ชื่อ NodeJS Installation ใน Jenkins
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
