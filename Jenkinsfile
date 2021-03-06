pipeline {
    agent {
        docker {
            image 'maven:3.6.2-jdk-13'
        }
    }

    environment {
        EMAIL_RECIPIANTS = 'ljolliff@cynerge.com'
        NEXUS_USER = credentials('nexus-user')
        NEXUS_PASS = credentials('nexus-pass')
        STATUS_SUCCESS = ''
        JENKINS_URL = "${JENKINS_URL}"
        JOB_NAME = "${JOB_NAME}"
        SONAR_TOKEN = credentials('shipyard-sonarqube')
        SONAR_PROJECT = 'shipyard-project-java'
        SONAR_SOURCE = 'java_webapp/src/main/java/com/puppet/sample/App.java'
        SONAR_REPORTS = 'java_webapp/target/surefire-reports'
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Unit Testing') {
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
        stage('Sonarqube Analysis') {
            environment {
                scannerHome = tool 'cynerge-sonarqube'
            }
            steps {
                withSonarQubeEnv('Cynerge Sonarqube') {
                    sh "printenv"
                    sh "ls $WORKSPACE/java_webapp/target"
                    sh "${scannerHome}/bin/sonar-scanner -Dsonar.login=$SONAR_TOKEN -Dsonar.projectKey=$SONAR_PROJECT -Dsonar.sources=$SONAR_SOURCE -Dsonar.junit.reportPaths=$SONAR_REPORTS"
                }
            }
        }
    }
}