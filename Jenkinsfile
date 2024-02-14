pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout your Java project from version control
                checkout scm
            }
        }

        stage('Build') {
            steps {
                script {
                    // Your existing Maven build steps
                    sh 'mvn clean install'
                }
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                script {
                    sh 'echo "Deploying to Tomcat server..."'
                    // Copy the WAR file to the target directory
                    sh 'docker cp target/*.war tomcatServer:/usr/local/tomcat/webapps/'
                }
            }
        }
    }
}
