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
                        def logFile = "${env.WORKSPACE}/unit_integration_tests.log"
                        writeFile file: logFile, text: currentBuild.rawBuild.getLog().join('\n')

                        // Send email notification after Test stage with the log file attached
                        emailext (
                            to: "anjithavarghese11@gmail.com",
                            subject: "Jenkins Job - ${env.JOB_NAME} #${env.BUILD_NUMBER} - Test Stage ${currentBuild.currentResult}",
                            body: """Build ${env.BUILD_NUMBER} on ${env.JOB_NAME} has completed the Test stage.
                            Status: ${currentBuild.currentResult}.
                            Please find the attached log for more details.""",
                            attachmentsPattern: "unit_integration_tests.log",
                            mimeType: 'text/plain'
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
                    script {
                       // Write the last 50 lines of the log to a file
                       def logFile = "${env.WORKSPACE}/build.log"
                       def logLines = currentBuild.getLog(50).join('\n')
                       writeFile file: logFile, text: logLines

                      // Send email notification with the log file attached
                      emailext (
                         to: "anjithavarghese11@gmail.com",
                         subject: "Jenkins Job - ${env.JOB_NAME} #${env.BUILD_NUMBER} - Stage ${currentBuild.currentResult}",
                         body: """Build ${env.BUILD_NUMBER} on ${env.JOB_NAME} has completed the stage.
                         Status: ${currentBuild.currentResult}.
                         Please find the attached log.""",
                         attachmentsPattern: "build.log",
                         mimeType: 'text/plain'
                        )
                    }
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
