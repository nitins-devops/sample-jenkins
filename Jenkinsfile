pipeline {
    agent any
    tools {
        jdk 'JDK-21'
        maven 'Maven-3.9.9'
    }
    options {
        disableConcurrentBuilds()

        // Keep only the last 10 builds
        buildDiscarder(
            logRotator(
                numToKeepStr: '2'
            )
        )

        // Add timestamps to console output
        timestamps()

        // Maximum time for the entire pipeline
        timeout(time: 1, unit: 'MINUTES')
    }    
    stages {
        stage('Test') {
            steps {
                echo "This is Test stage"
                powershell 'Start-Sleep -Seconds 90'
            }
        }
        stage('store') { 
            steps {
                echo "This is store stage" 
            }
        }
        stage('modify') { 
            steps {
                echo "This is store stage" 
            }
        }		
    }
}
