pipeline {
    //By Tristan Venter, For SIT223 - Professional Practice in IT
    //Task 6.1P
    agent any

     tools {
        maven 'Maven' 
    }
    
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                bat 'mvn clean package'  // Using Maven for building the project
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                bat 'mvn test'  // Run unit and integration tests
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo 'Performing Code Analysis...'
                //sh 'sonar:sonar'  // Using SonarQube for code analysis
            }
        }
        
        stage('Security Scan') {
            steps {
                echo 'Running Security Scan...'
                bat 'mvn dependency-check:check'  // Using OWASP Dependency Check for security scanning
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                //bat 'scp target/*.jar user@staging-server:/path/to/deploy'  // Example deployment command
                failure {
                    mail to: "vibrant.subbedl@gmail.com",
                    subject: "Test Stage Failed",
                    body: "The test stage failed. Please check the Jenkins logs."
                 }
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                bat 'mvn integration-test'  // Run tests on the staging environment
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                //bat 'scp target/*.jar user@production-server:/path/to/deploy'  // Example deployment command
            }
        }
    }
    
    post {
        success {
                mail to: "vibrant.subbedl@gmail.com",
                subject: "Test Stage Passed",
                body: "The test stage completed successfully."
        }
        failure {
                mail to: "vibrant.subbedl@gmail.com",
                subject: "Test Stage Failed",
                body: "The test stage failed. Please check the Jenkins logs."
        }
    }
}
