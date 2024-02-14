pipeline {
    agent any

    stages {
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
                    sh 'pwd'
                    // Create the target directory if it doesn't exist
                    sh 'mkdir -p /home/ayroid/Documents/warfiles'

                    // Copy the WAR file to the target directory
                    sh 'cp -f target/motiverse.war /home/ayroid/Documents/warfiles/'
                }
            }
        }
    }
}
