pipeline {
    // Defines the agent to run the pipeline on
    agent any

    stages {
        // building the code
        stage('Build') {
            steps {
                // Echoes a message indicating that the build process is starting
                echo "Building the code using Maven"
            }
        }

        // Stage for running unit and integration tests
        stage('Unit and Integration Tests') {
            steps {
                // Echoes a message indicating that unit and integration tests are being run
                echo "Running Unit and Integration Tests"
            }
            post {
                // Actions to perform after the stage has completed
                always {
                    script {
                        // Retrieve the status of the current build stage
                        def stageStatus = currentBuild.currentResult
                        // Send an email notification with the test results and log attachments
                        mail to: "roji.13804@gmail.com",
                             subject: "Unit and Integration Tests Stage: ${stageStatus}",
                             body: "The Unit and Integration Tests stage has completed with status: ${stageStatus}. Please find the attached logs for details.",
                             attachmentsPattern: '/target/surefire-reports/*.xml'
                    }
                }
            }
        }

        // Stage for performing code analysis
        stage('Code Analysis') {
            steps {
                // Echoes a message indicating that code analysis is being performed
                echo "Performing Code Analysis with SonarQube"
            }
        }

        // Stage for performing a security scan
        stage('Security Scan') {
            steps {
                // Echoes a message indicating that a security scan is being performed
                echo "Performing Security Scan with OWASP Dependency-Check"
            }
            post {
                // Actions to perform after the stage has completed
                always {
                    script {
                        // Retrieve the status of the current build stage
                        def stageStatus = currentBuild.currentResult
                        // Send an email notification with the security scan results and log attachments
                        mail to: "roji.13804@gmail.com",
                             subject: "Security Scan Stage: ${stageStatus}",
                             body: "The Security Scan stage has completed with status: ${stageStatus}. Please find the attached logs for details.",
                             attachmentsPattern: '/target/dependency-check-report.html'
                    }
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                // Echoes a message indicating that deployment to the staging server is starting
                echo "Deploying to Staging Server"
            }
        }

        // Stage for running integration tests on the staging environment
        stage('Integration Tests on Staging') {
            steps {
                // Echoes a message indicating that integration tests are being run on staging
                echo "Running Integration Tests on Staging"
            }
        }

        // Stage for deploying to the production server
        stage('Deploy to Production') {
            steps {
                // Echoes a message indicating that deployment to the production server is starting
                echo "Deploying to Production Server"
            }
        }
    }

    // Post-build actions
    post {
        // Actions to perform if the entire pipeline succeeds
        success {
            mail to: "roji.13804@gmail.com",
                 subject: "Pipeline Status: SUCCESS",
                 body: "The pipeline completed successfully."
        }

        // Actions to perform if the entire pipeline fails
        failure {
            mail to: "roji.13804@gmail.com",
                 subject: "Pipeline Status: FAILURE",
                 body: "The pipeline failed. Please check the Jenkins logs for more details."
        }
    }
}
