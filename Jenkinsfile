pipeline {
    agent any
    tools {
        maven 'M3'
    }
    stages {
        stage('清理') {
            steps {
                bat 'mvn clean'
            }
        }
        stage('编译') {
            steps {
                bat 'mvn compile'
            }
        }
        stage('打包') {
            steps {
                bat 'mvn package -DskipTests'
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: 'docs-web/target/*.war'
        }
    }
}