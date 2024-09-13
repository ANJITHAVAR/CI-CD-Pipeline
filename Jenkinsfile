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
                        // Capture the build log, write it to a file
                        def logContent = currentBuild.rawBuild.getLog(100).join('\n')
                        def logFile = "${env.WORKSPACE}/build.log"
                        writeFile file: logFile, text: logContent

                        // Send email with log file as an attachment
                        emailext(
                            to: "${RECIPIENT_EMAIL}",
                            subject: "Jenkins Job - ${env.JOB_NAME} #${env.BUILD_NUMBER} - Test Stage ${currentBuild.currentResult}",
                            body: """Build ${env.BUILD_NUMBER} on ${env.JOB_NAME} has completed the Test stage.
                            Status: ${currentBuild.currentResult}.
                            Logs are attached.""",
                            mimeType: 'text/plain',
                            attachmentsPattern: 'build.log'
                        )
                    }
                }
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan using OWASP ZAP'
            }
            post {
                always {
                    script {
                        // Send basic email without log attachment for now
                        emailext(
                            to: "${RECIPIENT_EMAIL}",
                            subject: "Jenkins Job - ${env.JOB_NAME} #${env.BUILD_NUMBER} - Security Scan Stage ${currentBuild.currentResult}",
                            body: """Build ${env.BUILD_NUMBER} on ${env.JOB_NAME} has completed the Security Scan stage.
                            Status: ${currentBuild.currentResult}"""
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
