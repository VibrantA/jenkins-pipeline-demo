pipeline {
    agent any
    //Hello! Watch this work.
    tools {
        maven 'Maven'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Using Maven to Build Project...'
                bat 'mvn clean package' // Using Maven for building the project (Testing)
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Using Maven to Run Unit and Initiate Integration Tests...'
                bat 'mvn test' // Run unit and integration tests through Maven
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Using Sonar to Perform Code Analysis...'
                // Uncomment and configure as needed: sh 'sonar:sonar'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Using Maven to Run Security Scan...'
                bat 'mvn dependency-check:check' // Using Maven OWASP Dependency Check for security scanning
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Using Maven -> Deploying to Staging...'
                // Example deployment command, configure as needed: bat 'scp target/*.jar user@staging-server:/path/to/deploy'
            }
        }

        stage('Running Maven Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                bat 'mvn integration-test' // Run tests on the staging environment
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Using Maven -> Deploying to Production...'
                // Example deployment command, configure as needed: bat 'scp target/*.jar JohnDoe@git-server:/path/to/deploy'
            }
        }
    }

    post {
        always {
            script {
                // Saving the last 100 lines of the log to a temporary file
                def logFile = "build-${env.BUILD_NUMBER}-log.txt"
                writeFile file: logFile, text: currentBuild.rawBuild.getLog(100).join("\n")
                
                // Email with attachment
                emailext (
                    subject: "${currentBuild.fullDisplayName} - Build #${currentBuild.number} - ${currentBuild.result}",
                    body: "Please find the build log attached.",
                    to: 'vibrant.subbedl@gmail.com',
                    attachmentsPattern: logFile
                )
            }
        }
    }
}
