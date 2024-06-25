pipeline {
    agent any

    tools {
        // Install the Maven version configured in Jenkins global tools configuration
        maven 'Maven 3.6.3'
        jdk 'JDK 21' // Adjust to the appropriate JDK version if needed
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the GitHub repository
                git url: 'https://github.com/Germain-L/exo8testunitaire.git', branch: 'main'
            }
        }
        stage('Build') {
            steps {
                // Run the Maven build
                sh 'mvn clean install'
            }
        }
        stage('Test') {
            steps {
                // Run the Maven tests
                sh 'mvn test'
            }
            post {
                // Archive the test results
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Package') {
            steps {
                // Package the application
                sh 'mvn package'
            }
            post {
                // Archive the built artifact
                always {
                    archiveArtifacts artifacts: 'target/*.jar', allowEmptyArchive: true
                }
            }
        }
    }

    post {
        // Notify if the build was successful or failed
        success {
            echo 'Build and Tests Successful!'
        }
        failure {
            echo 'Build or Tests Failed!'
        }
    }
}
