pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Starting the build process using Maven"
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo "Executing Unit and Integration Tests"
                
            }
            post {
                always {
                    script {
                        // Get the result of the current stage
                        def stageStatus = currentBuild.currentResult
                        // Send an email notification with the stage status and log attachments
                        emailext to: "roji.13804@gmail.com",
                                 subject: "Unit and Integration Tests Stage: ${stageStatus}",
                                 body: "The Unit and Integration Tests stage has completed with status: ${stageStatus}. The full logs are attached.",
                                 attachLog: true,
                                 mimeType: 'text/html'
                    }
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo "Analyzing code quality using SonarQube"
            }
        }

        stage('Security Scan') {
            steps {
                echo "Running security checks using OWASP Dependency-Check"
            }
            post {
                always {
                    script {
                        // Get the result of the current stage
                        def stageStatus = currentBuild.currentResult
                        // Send an email notification with the stage status and log attachments
                        emailext to: "roji.13804@gmail.com",
                                 subject: "Security Scan Stage: ${stageStatus}",
                                 body: "The Security Scan stage has completed with status: ${stageStatus}. The full logs are attached.",
                                 attachLog: true,
                                 mimeType: 'text/html'
                    }
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Deploying application to the Staging Server"
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo "Performing Integration Tests on the Staging environment"
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Deploying application to the Production Server"
            }
        }
    }

    post {
        success {
            // Send an email notification if the pipeline completes successfully
            emailext to: "roji.13804@gmail.com",
                     subject: "Pipeline Status: SUCCESS",
                     body: "The pipeline completed successfully. The full logs are attached.",
                     attachLog: true,
                     mimeType: 'text/html'
        }

        failure {
            // Send an email notification if the pipeline fails
            emailext to: "roji.13804@gmail.com",
                     subject: "Pipeline Status: FAILURE",
                     body: "The pipeline failed. Please check the attached logs for more details.",
                     attachLog: true,
                     mimeType: 'text/html'
        }
    }
}
