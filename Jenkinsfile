pipeline {
    agent any
    tools {
        jdk 'JDK21'
        maven 'Maven3'
    }
    stages {
        stage('拉取代码') {
            steps {
                checkout scm
            }
        }
        stage('Maven 构建') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }
        stage('PMD 代码检查') {
            steps {
                sh 'mvn pmd:pmd'
            }
            post {
                always {
                    pmd pattern: 'target/pmd.xml'
                }
            }
        }
        stage('运行单元测试') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('生成测试报告') {
            steps {
                sh 'mvn surefire-report:report'
            }
        }
        stage('生成 JavaDoc') {
            steps {
                sh 'mvn javadoc:javadoc'
            }
        }
    }
    post {
        success { echo '✅ 构建成功' }
        failure { echo '❌ 构建失败' }
    }
}