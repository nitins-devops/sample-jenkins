pipeline {
    agent any
    tools {
        jdk 'JDK-21'
        maven 'Maven-3.9.9'
    }    
    stages {
        stage('Test') {
            steps {
                echo "This is Test stage"
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
