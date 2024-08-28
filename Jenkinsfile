pipeline {
    agent any
    
    environment {
        EMAIL_RECIPIENT = 'roji.13804@gmail.com'
    }
    
    stages {
        stage('Build') {
            steps {
                echo "Building the code using Maven"
                sh 'mvn clean package'
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo "Running unit tests using JUnit and integration tests"
                sh 'mvn test'
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo "Performing code analysis using SonarQube"
                sh 'mvn sonar:sonar'
            }
        }
        
        stage('Security Scan') {
            steps {
                echo "Performing security scan using OWASP Dependency-Check"
                sh 'dependency-check.sh --project "My Project" --out reports'
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo "Deploying to staging server"
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo "Running integration tests on staging environment"
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo "Deploying to production server"
            }
        }
    }
    
    post {
        success {
            mail to: EMAIL_RECIPIENT,
                 subject: "Pipeline Success: ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                 body: "The build was successful.\n\nBuild details:\n${env.BUILD_URL}",
                 attachmentsPattern: '**/target/*.jar' 
        }
        failure {
            mail to: EMAIL_RECIPIENT,
                 subject: "Pipeline Failed: ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                 body: "The build failed.\n\nBuild details:\n${env.BUILD_URL}\n\nLogs:\n${env.BUILD_URL}console",
                 attachmentsPattern: '**/target/*.log' 
        }
    }
}
