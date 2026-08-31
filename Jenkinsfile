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
        timeout(time: 30, unit: 'MINUTES')
    }
    parameters {
        choice(
            name: 'ENVIRONMENT',
            choices: ['dev', 'sit', 'bat', 'nft', 'ite', 'prod'],
            description: 'Environment to deploy to'
        )
        choice(
            name: 'BUILD',
            choices: ['NO', 'YES'],
            description: 'Deploy after successful build?'
        )
        booleanParam(
            name: 'RUN_TESTS',
            defaultValue: true,
            description: 'Run unit tests'
        )
    }    
    stages {
        stage('Test') {
            steps {
                script {
                    echo "This is Test stage"
                    if(params.ENVIRONMENT == "dev"){
                        echo "This is dev environment"
                    } else if (params.ENVIRONMENT == "sit") {
                        echo "This is sit environment"
                    } else {
                        echo "You have selected - ${params.ENVIRONMENT}"
                    }
                }
            }
        }
        stage('store') {
            when {
                expression {
                    params.ENVIRONMENT != 'sit'
                }
            }
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
