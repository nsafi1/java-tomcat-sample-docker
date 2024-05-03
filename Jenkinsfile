pipeline {
    agent any
    stages {
        stage('Build Application') {
            steps {
                // Build the Java application using Maven
                bat 'mvn -f pom.xml clean package'
            }
            post {
                success {
                    // Archive the WAR artifact
                    echo "Now Archiving the Artifacts...."
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }

        stage('Create Tomcat Docker Image'){
            steps {
                // Print current working directory and list all files (for debugging)
                bat "cd"
                bat "dir"
                
                // Build the Docker image with a tag including Jenkins build ID
                bat "docker build . -t tomcatsamplewebapp:%BUILD_ID%"
            }
        }
    }
}