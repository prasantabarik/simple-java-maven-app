pipeline {
    agent any
    tools {
        maven 'maven'
    } 
    options {
        skipStagesAfterUnstable()
    }
    stages {
       stage('Build') {
           steps {
                bat 'mvn -B -DskipTests clean package'
            }
        }
       stage('SonarAnalysis') {
            steps {
                bat 'mvn sonar:sonar -Dsonar.host.url=http://localhost:9000 -Dsonar.login=admin -Dsonar.password=admin'
            }
        }
        stage('Test') {
            steps {
                bat 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') { 
            steps {
                bat './jenkins/scripts/deliver.sh' 
            }
        }
    }
}
