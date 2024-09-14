pipeline {
    agent any

    environment {
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
                    script {
                        // Write the log to a file
                        def logFile = "${env.WORKSPACE}/test.log"
                        writeFile file: logFile, text: currentBuild.rawBuild.getLog().join('\n')

                        // Send email notification with log attachment
                        emailext (
                            to: "${env.RECIPIENT_EMAIL}",
                            subject: "Jenkins Job - ${env.JOB_NAME} #${env.BUILD_NUMBER} - Test Stage ${currentBuild.currentResult}",
                            body: """Build ${env.BUILD_NUMBER} on ${env.JOB_NAME} has completed the Test stage.
                                     Status: ${currentBuild.currentResult}
                                     The full build log is attached.""",
                            attachmentsPattern: "test.log",
                            mimeType: 'text/html'
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
                        // Write the log to a file
                        def logFile = "${env.WORKSPACE}/security_scan.log"
                        writeFile file: logFile, text: currentBuild.rawBuild.getLog().join('\n')

                        // Send email notification with log attachment
                        emailext (
                            to: "${env.RECIPIENT_EMAIL}",
                            subject: "Jenkins Job - ${env.JOB_NAME} #${env.BUILD_NUMBER} - Security Scan Stage ${currentBuild.currentResult}",
                            body: """Build ${env.BUILD_NUMBER} on ${env.JOB_NAME} has completed the Security Scan stage.
                                     Status: ${currentBuild.currentResult}
                                     The full build log is attached.""",
                            attachmentsPattern: "security_scan.log",
                            mimeType: 'text/html'
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
