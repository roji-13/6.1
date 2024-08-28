pipeline {
    agent any
    
    environment {
        EMAIL_RECIPIENT = 'roji.13804@gmail.com'
    }
    
    stages {
        stage('Build') {
            steps {
                echo 'Building the code...'
                // Example of using Maven for the build stage
                echo 'mvn clean package'
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                // Example of using JUnit for unit tests
                echo 'mvn test'
                // Add integration test commands here
                echo 'Integration test commands here'
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo 'Performing code analysis...'
                // Example of using SonarQube for code analysis
                echo 'mvn sonar:sonar'
            }
        }
        
        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                // Example of using OWASP Dependency-Check for security scanning
                echo 'dependency-check.sh --project "My Project" --out reports'
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging...'
                // Add deployment commands here
                echo 'Deployment commands for staging here'
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                // Add integration test commands here
                echo 'Integration test commands for staging here'
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production...'
                // Add deployment commands here
                echo 'Deployment commands for production here'
            }
        }
    }
    
    post {
        success {
            emailext (
                to: EMAIL_RECIPIENT,
                subject: "Build Successful: ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                body: "The build was successful.\n\nBuild details:\n${env.BUILD_URL}\n\nLogs:\n${env.BUILD_URL}console",
                attachLog: true
            )
        }
        failure {
            emailext (
                to: EMAIL_RECIPIENT,
                subject: "Build Failed: ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                body: "The build failed.\n\nBuild details:\n${env.BUILD_URL}\n\nLogs:\n${env.BUILD_URL}console",
                attachLog: true
            )
        }
    }
}
