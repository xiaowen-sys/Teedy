pipeline {
    agent any
    stages {
        stage('Clean') {
            steps {
                bat 'mvn clean'
            }
        }
        stage('Compile') {
            steps {
                bat 'mvn compile'
            }
        }
        stage('Package') {
            steps {
                bat 'mvn package -DskipTests'
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: 'target/*.war', fingerprint: true
        }
    }
}