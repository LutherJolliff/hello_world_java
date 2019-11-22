pipeline {
    agent {
        docker {
            image 'maven:3.6.2-jdk-13'
        }
    }
    stages {
        stage('Clean Packages') {
            steps {
                sh 'mvn --version'
                sh 'java --version'
                sh 'mvn clean package'
            }
        }
    }
}