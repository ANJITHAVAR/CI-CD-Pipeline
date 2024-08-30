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
            }
            post {
                always {
                    script {
                        // Write the log to a file
                        def logFile = "${env.WORKSPACE}/build.log"
                        writeFile file: logFile, text: currentBuild.rawBuild.getLog().join('\n')

                        // Send the email with the log file attached
                        emailext (
                        to: "anjithavarghese11@gmail.com",
                        subject: "Jenkins Job - ${env.JOB_NAME} #${env.BUILD_NUMBER} - Test Stage ${currentBuild.currentResult}",
                        body: """Build ${env.BUILD_NUMBER} on ${env.JOB_NAME} has completed the Test stage.
                        Status: ${currentBuild.currentResult}
                        The full build log is attached.""",
                        mimeType: 'text/plain',
                        attachmentsPattern: "build.log"
                        )
                    }
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
                     mail to: "anjithavarghese11@gmail.com",
                     subject: "Jenkins Job - ${JOB_NAME} #${BUILD_NUMBER} - Security Scan Stage ${currentBuild.currentResult}",
                     body: """Build ${BUILD_NUMBER} on ${JOB_NAME} has completed the Security Scan stage.
                                 Status: ${currentBuild.currentResult}"""
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
