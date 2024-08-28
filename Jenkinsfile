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
                sh 'mvn clean package'
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                // Example of using JUnit for unit tests
                sh 'mvn test'
                // Add integration test commands here
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo 'Performing code analysis...'
                // Example of using SonarQube for code analysis
                sh 'mvn sonar:sonar'
            }
        }
        
        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                // Example of using OWASP Dependency-Check for security scanning
                sh 'dependency-check.sh --project "My Project" --out reports'
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging...'
                // Add deployment commands here
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                // Add integration test commands here
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production...'
                // Add deployment commands here
            }
        }
    }
    
    post {
        success {
            mail to: EMAIL_RECIPIENT,
                 subject: "Build Successful: ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                 body: "The build was successful.\n\nBuild details:\n${env.BUILD_URL}",
                 attachLog: true
        }
        failure {
            mail to: EMAIL_RECIPIENT,
                 subject: "Build Failed: ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                 body: "The build failed.\n\nBuild details:\n${env.BUILD_URL}\n\nLogs:\n${env.BUILD_URL}console",
                 attachLog: true
        }
    }
}
