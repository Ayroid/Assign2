pipeline {
    agent any

    environment {
        // Define any environment variables needed
        DOCKER_IMAGE_NAME = 'mvsAssign2'
        TOMCAT_IMAGE_NAME = 'tomcat:latest'
        CONTAINER_NAME = 'mvsAssign2-container'
        WAR_FILE = 'mvsAssign2.war'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout your Java project from version control
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Build your Java project (e.g., using Maven)
                sh 'mvn clean package'
            }
        }

        stage('Containerize') {
            steps {
                // Build Docker image for Java application
                script {
                    docker.build(DOCKER_IMAGE_NAME, "--build-arg JAR_FILE=target/${WAR_FILE} .")
                }
            }
        }

        stage('Start Tomcat Container') {
            steps {
                // Start the Tomcat container
                script {
                    docker.image(TOMCAT_IMAGE_NAME).withRun('-d -p 8080:8080 --name ${CONTAINER_NAME}')
                }
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                // Copy the WAR file to the Tomcat container
                script {
                    docker.cp("${DOCKER_IMAGE_NAME}:${WAR_FILE}", "${CONTAINER_NAME}:/usr/local/tomcat/webapps/")
                }
            }
        }
    }

    post {
        always {
            // Cleanup: Stop and remove the Tomcat container
            script {
                docker.stop(CONTAINER_NAME)
                docker.remove(CONTAINER_NAME)
            }
        }
    }
}
