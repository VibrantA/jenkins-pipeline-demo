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
                bat 'bat clean package'  // Using Maven for building the project
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                bat 'bat test'  // Run unit and integration tests
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo 'Performing Code Analysis...'
                bat 'bat sonar:sonar'  // Using SonarQube for code analysis
            }
        }
        
        stage('Security Scan') {
            steps {
                echo 'Running Security Scan...'
                bat 'bat dependency-check:check'  // Using OWASP Dependency Check for security scanning
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                bat 'scp target/*.jar user@staging-server:/path/to/deploy'  // Example deployment command
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                bat 'bat integration-test'  // Run tests on the staging environment
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                bat 'scp target/*.jar user@production-server:/path/to/deploy'  // Example deployment command
            }
        }
    }
    
    post {
        success {
            emailext(
                subject: "Test Stage Passed",
                body: "The test stage completed successfully.",
                recipientProviders: [[$class: 'DevelopersRecipientProvider']]
            )
        }
        failure {
            emailext(
                subject: "Test Stage Failed",
                body: "The test stage failed. Please check the Jenkins logs.",
                recipientProviders: [[$class: 'DevelopersRecipientProvider']]
            )
        }
    }
}
