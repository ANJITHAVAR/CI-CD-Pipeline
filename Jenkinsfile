pipeline {
    agent any

    environment {
        RECIPIENT_EMAIL = 'anjithavarghese11@gmail.com'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the code using Maven'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests using JUnit'
            }
            post {
                always {
                    script {
                        // Capture the last 100 lines of the log
                        def logContent = currentBuild.rawBuild.getLog(100).join('\n')
                        
                        // Write the log to a file
                        writeFile file: 'test-stage-log.txt', text: logContent

                        // Send the email notification with the log file attached
                        emailext(
                            to: "${RECIPIENT_EMAIL}",
                            subject: "Jenkins Job - ${env.JOB_NAME} #${env.BUILD_NUMBER} - Test Stage ${currentBuild.currentResult}",
                            body: """<p>Build ${env.BUILD_NUMBER} on ${env.JOB_NAME} has completed the Test stage.</p>
                                     <p>Status: ${currentBuild.currentResult}</p>
                                     <p>Logs are attached.</p>""",
                            mimeType: 'text/html',
                            attachmentsPattern: 'test-stage-log.txt'
                        )
                    }
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing code quality using SonarQube'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan using OWASP ZAP'
            }
            post {
                always {
                    script {
                        // Capture the last 100 lines of the log
                        def logContent = currentBuild.rawBuild.getLog(100).join('\n')
                        
                        // Write the log to a file
                        writeFile file: 'security-scan-log.txt', text: logContent

                        // Send the email notification with the log file attached
                        emailext(
                            to: "${RECIPIENT_EMAIL}",
                            subject: "Jenkins Job - ${env.JOB_NAME} #${env.BUILD_NUMBER} - Security Scan Stage ${currentBuild.currentResult}",
                            body: """<p>Build ${env.BUILD_NUMBER} on ${env.JOB_NAME} has completed the Security Scan stage.</p>
                                     <p>Status: ${currentBuild.currentResult}</p>
                                     <p>Logs are attached.</p>""",
                            mimeType: 'text/html',
                            attachmentsPattern: 'security-scan-log.txt'
                        )
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed'
        }
    }
}
