pipeline {

    agent any

    options {
        buildDiscarder logRotator( 
                    daysToKeepStr: '16', 
                    numToKeepStr: '10'
            )
    }

    stages {
        
        stage('Cleanup Workspace') {
            steps {
                cleanWs()
                sh """
                echo "Cleaned Up Workspace For Project"
                """
            }
        }

        stage('Code Checkout') {
            steps {
                checkout([$class: 'GitSCM', 
                branches: [[name: '*/main']],
                extensions: [], 
                userRemoteConfigs: [[url: 'https://github.com/aafetorgbor/multibranch-pipeline.git']]])
            }
        }

        
        stage(' Build') {
             when {
                branch 'develop'
            }
            steps {
                sh """
                echo "This only run when we are on the develop branch"
                """
            }
        }

       
        stage('For PR') {
            when {
                branch 'PR-*'
            }
            steps {
                sh """
                echo "This stage only run for PR"
                """

            }
        }

    }   
}
