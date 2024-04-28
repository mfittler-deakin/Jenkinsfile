pipeline {
    agent any
    environment {
        BUILD_TOOL = "Maven"
        UNIT_AND_INTEGRATION_TESTS_TOOL = "Apache JMeter"
        CODE_ANALYSIS_TOOL = "JArchitect"
        SECURITY_SCAN_TOOL = "SonaType Nexus"
        DEPLOY_TOOL = "AWS EC2 instance"
    }
    stages {
        stage('Build') {
            steps {
                echo "Compile and package code using ${BUILD_TOOL}"
                echo "Testing SCM polling"
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo "Run unit tests using ${UNIT_AND_INTEGRATION_TESTS_TOOL}"
            }
            post {
                always {
                    emailext attachLog: true,
                    to: "m88792210@gmail.com",
                    subject: "Unit and Integration Tests - ${currentBuild.currentResult}",
                    body: "Unit and Integration Tests - ${currentBuild.currentResult}"
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo "Check the quality of the code using ${CODE_ANALYSIS_TOOL}"
            }   
        }
        stage('Security Scan') {
            steps {
                echo "perform a security scan on the code using ${SECURITY_SCAN_TOOL} to identify any vulnerabilities."
            }
            post {
                always {
                    emailext attachLog: true,
                    to: "m88792210@gmail.com",
                    subject: "Security Scan - ${currentBuild.currentResult}",
                    body: "Security Scan - ${currentBuild.currentResult}"
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo "Deploy the application to a staging server - ${DEPLOY_TOOL}"
            }   
        }
        stage('Integration Tests on Staging') {
            steps {
                echo "Run integration tests on the staging environment to ensure the application functions as expected in a production-like environment using ${CODE_ANALYSIS_TOOL}"
            }   
        }
        stage('Deploy to Production') {
            steps {
                echo "Deploy the application to a production server ${DEPLOY_TOOL}"
            }   
        }
    }
}
