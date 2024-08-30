pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building the code using Maven'
                // Tool: Maven
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests using JUnit'
                // Tools: JUnit for unit tests, Selenium for integration tests
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing code quality using SonarQube'
                // Tool: SonarQube
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan using OWASP ZAP'
                // Tool: OWASP ZAP
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying application to staging environment (AWS EC2)'
                // Deployment to AWS EC2
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging environment'
                // Tools: Same as integration test tools used earlier
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying application to production environment (AWS EC2)'
                // Final production deployment
            }
        }
    }
    post {
        always {
            echo 'Pipeline completed'
        }
    }
}
