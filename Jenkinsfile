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
        always {
            script {
                // Capture the console output and store it in a variable
                def buildLog = currentBuild.rawBuild.getLog(1000).join('\n')
                
                // Send an email with the entire log as the body
                emailext(
                    subject: "Pipeline Build: ${currentBuild.currentResult} - ${env.JOB_NAME} ${env.BUILD_NUMBER}",
                    body: """<p>Build Status: ${currentBuild.currentResult}</p>
                             <p>Job: ${env.JOB_NAME} - Build #: ${env.BUILD_NUMBER}</p>
                             <p>Build Log:</p>
                             <pre>${buildLog}</pre>""",
                    mimeType: 'text/html',
                    to: "vibrant.subbedl@gmail.com"
                )
            }
        }
    }
}
