pipeline {
    agent any

     tools {
        maven 'Maven' 
    }
    
    stages {
        stage('Build') {
            steps {
                echo 'Using Maven to Build Project...'
                bat 'mvn clean package'  // Using Maven for building the project
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo 'Using Maven to Run Unit and Initiate Integration Tests...'
                bat 'mvn test'  // Run unit and integration tests through Maven
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo 'Using Sonar to Perform Code Analysis...'
                //sh 'sonar:sonar'  // Here we would use SonarQube for code analysis
            }
        }
        
        stage('Security Scan') {
            steps {
                echo 'Using Maven to Run Security Scan...'
                bat 'mvn dependency-check:check'  // Using Maven OWASP Dependency Check for security scanning
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo 'Using Maven -> Deploying to Staging...'
                //bat 'scp target/*.jar user@staging-server:/path/to/deploy'  // Example deployment command
            }
        }
        
        stage('Running Maven Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                bat 'mvn integration-test'  // Run tests on the staging environment
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Using Maven -> Deploying to Production...'
                //bat 'scp target/*.jar JohnDoe@git-server:/path/to/deploy'  // Example deployment command (Using Maven and Secure Copy Protocol (SCP) to send the project to a remote server
            }
        }
    }
    
    post {
        success { //In the case of success, send an email to the specified email to alert of success.
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
