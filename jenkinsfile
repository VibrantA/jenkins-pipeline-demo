pipeline {
    //By Tristan Venter, For SIT223 - Professional Practice in IT
    //Task 6.1P
    agent any
    
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                sh 'mvn clean package'  // Using Maven for building the project
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                sh 'mvn test'  // Run unit and integration tests
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo 'Performing Code Analysis...'
                sh 'mvn sonar:sonar'  // Using SonarQube for code analysis
            }
        }
        
        stage('Security Scan') {
            steps {
                echo 'Running Security Scan...'
                sh 'mvn dependency-check:check'  // Using OWASP Dependency Check for security scanning
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                sh 'scp target/*.jar user@staging-server:/path/to/deploy'  // Example deployment command
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                sh 'mvn integration-test'  // Run tests on the staging environment
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                sh 'scp target/*.jar user@production-server:/path/to/deploy'  // Example deployment command
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
