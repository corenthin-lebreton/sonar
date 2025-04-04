pipeline {
    agent any
    tools {
        maven 'Maven 3.9.9'
    }

    stages {
        stage('checkout') {
            steps {
                git 'https://github.com/ScaleSec/vulnado'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    def mvnHome = tool 'Maven 3.9.9' //
                    withSonarQubeEnv('Sonarqube') {
                    sh "${mvnHome}/bin/mvn clean verify sonar:sonar -
                    Dsonar.projectKey=Vulnado -Dsonar.projectName='Vulnado'"
                }
            }
        }

    } 
}
