pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the code'
            }
        }
        stage('Test') {
            steps {
                echo 'Running Tests'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying Application'
            }
        }
    }

    post {
        always {
            script {
                // Capture and archive the log
                def buildLog = currentBuild.rawBuild.getLog(100)  // get last 100 lines
                writeFile file: 'build.log', text: buildLog.join('\n')
                archiveArtifacts artifacts: 'build.log'

                // Send email notification with the build log attached
                emailext body: """
                    Build ${env.JOB_NAME} #${env.BUILD_NUMBER} finished.
                    Status: ${currentBuild.currentResult}.
                    Please see attached log for more details.
                    """,
                    subject: "Build ${env.JOB_NAME} #${env.BUILD_NUMBER} - ${currentBuild.currentResult}",
                    to: 'your-email@example.com',
                    attachLog: true
            }
        }
    }
}
