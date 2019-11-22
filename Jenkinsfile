pipeline {
    agent {
        docker {
            image 'maven:3.6.2-jdk-13'
        }
    }
    stages {
        stage('Sonarqube Scan') {
            steps {
                withSonarQubeEnv() {
                    sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.6.0.1398:sonar'
                }
            }
        }
        stage('Clean Packages') {
            steps {
                sh 'mvn --version'
                sh 'java --version'
                sh 'mvn clean package'
            }
        }
    }
}