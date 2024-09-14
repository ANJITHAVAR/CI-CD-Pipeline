Jenkinsfile 

pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the code using Maven'
                echo 'Tool: Maven'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests using JUnit'
                echo 'Tools: JUnit for unit tests, Selenium for integration tests'
                emailext (attachLog: true, body: '''Build ${env.BUILD_NUMBER} on ${env.JOB_NAME} has completed the Test stage.
Status: ${currentBuild.currentResult}''', subject: 'Jenkins Job - ${env.JOB_NAME} #${env.BUILD_NUMBER} - Test Stage ${currentBuild.currentResult}', to: 'anjithavarghese11@gmail.com')
            }
                    }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing code quality using SonarQube'
                echo 'Tool: SonarQube'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan using OWASP ZAP'
                echo 'Tool: OWASP ZAP'
                emailext (attachLog: true, body: '''Build ${env.BUILD_NUMBER} on ${env.JOB_NAME} has completed the Security Scan stage.
Status: ${currentBuild.currentResult}''', subject: 'Jenkins Job - ${env.JOB_NAME} #${env.BUILD_NUMBER} - Security Scan Stage ${currentBuild.currentResult}', to: 'anjithavarghese11@gmail.com')
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
                echo 'Tools: Selenium for integration tests'
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
