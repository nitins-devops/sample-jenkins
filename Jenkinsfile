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
            name: 'Deploy',
            choices: ['NO', 'YES'],
            description: 'Deploy after successful build?'
        )
        booleanParam(
            name: 'RUN_TESTS',
            defaultValue: true,
            description: 'Run unit tests'
        )
    }
    environment {
        APP_NAME = 'my-app'
        ENV = "${params.ENVIRONMENT}"
        DEP = "${params.Deploy}"
        TEST = "${params.RUN_TESTS}"        
    }    
    stages {        
        stage('Test') {
            steps {
                script {
                    echo "This is Test stage"
                    if( (ENV == "dev") && (TEST == "true") && (DEP == "YES") ){
                        echo "This is dev environment and want to execute test"
                    } else if ((ENV == "sit") && (TEST == "false") && (DEP == "NO") ) {
                        echo "This is sit environment and don't want to execute test"
                    } else {
                        echo "You have selected - ${ENV} and Test - ${TEST} - app name - ${APP_NAME}"
                        APP_NAME = "Updated value"                        
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
                script {
                    echo "This is store stage"
                    echo "app name - ${APP_NAME}"
                    APP_NAME = "Updated again"
                }
            }
        }
        stage('modify') { 
            steps {
                echo "This is modify stage"
                echo "app name - ${APP_NAME}"
            }
        }
        stage('Send Email') {
            steps {
                emailext(
                    subject: "Jenkins Build - ${currentBuild.currentResult}",
                    body: """
                        Hello,
        
                        Jenkins build has completed.
        
                        Job: ${env.JOB_NAME}
                        Build Number: ${env.BUILD_NUMBER}
                        Status: ${currentBuild.currentResult}
                        Build URL: ${env.BUILD_URL}
        
                        Regards,
                        Jenkins
                    """,
                    to: 'amberambreen01@gmail.com'
                )
            }
        }        
    }
    post {
        always {
            echo "Build number: ${currentBuild.number}"
            echo "Build result: ${currentBuild.result}"
            echo "Build display name: ${currentBuild.displayName}"
            echo "Build URL: ${currentBuild.absoluteUrl}"
            echo "Build duration: ${currentBuild.durationString}"
        }
    }    
}
