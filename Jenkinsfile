pipeline {
    agent {
        docker {
            image 'maven:3.6.2-jdk-13'
        }
    }
    stages {
        // stage('Sonarqube Scan') {
        //     steps {
        //         withSonarQubeEnv(installationName: 'AWS-Sonarqube') {
        //             sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.6.0.1398:sonar'
        //         }
        //     }
        // }
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
                sh 'ls'
                sh 'pwd'
            }
            post {
                always {
                    junit "java_webapp*/target/surefire-reports/*.xml"
                }
            }
        }
    }
}