pipeline {
    agent any
    
    environment {
        EMAIL_RECIPIENT = 'roji.13804@gmail.com'
    }
    
    stages {
        stage('Build') {
            steps {
                script {
                    echo 'Building the code...'
                    // Example of using Maven to build the project
                    sh 'mvn clean package'
                }
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                script {
                    echo 'Running unit and integration tests...'
                    // Example of using Maven for unit tests and adding integration test commands
                    sh 'mvn test'
                    // Example integration test commands
                    // sh 'mvn verify'
                }
            }
        }
        
        stage('Code Analysis') {
            steps {
                script {
                    echo 'Performing code analysis...'
                    // Example of using SonarQube for code analysis
                    // Make sure SonarQube is properly configured in your Jenkins instance
                    sh 'mvn sonar:sonar'
                }
            }
        }
        
        stage('Security Scan') {
            steps {
                script {
                    echo 'Performing security scan...'
                    // Example of using OWASP Dependency-Check
                    // Make sure the Dependency-Check CLI is available in your Jenkins environment
                    sh 'dependency-check.sh --project "My Project" --out reports'
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                script {
                    echo 'Deploying to staging...'
                    // Example deployment script to a staging server
                    // Replace with your actual deployment commands
                    // Example: Using AWS CLI to deploy
                    // sh 'aws deploy create-deployment --application-name MyApp --deployment-group-name Staging --s3-location bucket=mybucket,key=myapp.zip'
                }
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                script {
                    echo 'Running integration tests on staging...'
                    // Example integration tests in the staging environment
                    // Adjust commands based on your staging environment
                    // sh 'curl -X POST http://staging-server-url/run-tests'
                }
            }
        }
        
        stage('Deploy to Production') {
            steps {
                script {
                    echo 'Deploying to production...'
                    // Example deployment script to a production server
                    // Replace with your actual deployment commands
                    // Example: Using AWS CLI to deploy
                    // sh 'aws deploy create-deployment --application-name MyApp --deployment-group-name Production --s3-location bucket=mybucket,key=myapp.zip'
                }
            }
        }
    }
    
    post {
        success {
            emailext(
                to: EMAIL_RECIPIENT,
                subject: "Pipeline Success: ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                body: "The build was successful.\n\nBuild details:\n${env.BUILD_URL}",
                attachmentsPattern: '**/target/*.jar' // Adjust pattern as necessary
            )
        }
        failure {
            emailext(
                to: EMAIL_RECIPIENT,
                subject: "Pipeline Failed: ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                body: "The build failed.\n\nBuild details:\n${env.BUILD_URL}\n\nLogs:\n${env.BUILD_URL}console",
                attachmentsPattern: '**/target/*.log' // Adjust pattern as necessary
            )
        }
    }
}
