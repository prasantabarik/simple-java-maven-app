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
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('SonarAnalysis') {
            steps {
                sh 'mvn sonar:sonar -Dsonar.host.url=http://192.168.99.100:9000 -Dsonar.login=admin -Dsonar.password=admin'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') { 
            steps {
                sh './jenkins/scripts/deliver.sh' 
            }
        }
    }
}
