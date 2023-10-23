pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Check out the source code from your version control system
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Set the Maven home (adjust the path accordingly)
                def mavenHome = tool name: 'Maven', type: 'maven'

                // Use the 'sh' step to execute shell commands
                sh "${mavenHome}/bin/mvn clean package"

                 // Use the 'sh' step to execute shell commands
                sh "${mavenHome}/bin/mvn clean intsall"
            }
        }

        stage('Test') {
            steps {
                // Run tests if needed (modify this command as per your project's testing strategy)
                sh "${mavenHome}/bin/mvn test"
            }
        }

        stage('Package') {
            steps {
                // Create the application package (e.g., JAR or WAR)
                sh "${mavenHome}/bin/mvn package"
            }
        }
    }

    post {
        success {
            archiveArtifacts(artifacts: '**/target/*.jar', allowEmptyArchive: true)
            // You can also deploy your application here if needed
        }

        failure {
            // Handle failure, send notifications, or take other actions
        }
    }
}
