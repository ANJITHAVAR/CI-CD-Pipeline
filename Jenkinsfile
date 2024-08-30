pipeline {
    agent any

    environment {
        // Specify the email address to send notifications
        RECIPIENT_EMAIL = 'anjithavarghese11@gmail.com'
    }
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
            }
            post {
                always {
                    // Send email notification after Test stage
                    emailext (
                        subject: "Jenkins Job - ${JOB_NAME} #${BUILD_NUMBER} - Test Stage ${currentBuild.currentResult}",
                        body: """<p>Build ${BUILD_NUMBER} on ${JOB_NAME} has completed the Test stage.</p>
                                 <p>Status: ${currentBuild.currentResult}</p>""",
                        to: "${env.RECIPIENT_EMAIL}",
                        attachLog: true
                    )
                }
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
            }
            post {
                always {
                    // Send email notification after Security Scan stage
                    emailext (
                        subject: "Jenkins Job - ${JOB_NAME} #${BUILD_NUMBER} - Security Scan Stage ${currentBuild.currentResult}",
                        body: """<p>Build ${BUILD_NUMBER} on ${JOB_NAME} has completed the Security Scan stage.</p>
                                 <p>Status: ${currentBuild.currentResult}</p>""",
                        to: "${env.RECIPIENT_EMAIL}",
                        attachLog: true
                    )
                }
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
