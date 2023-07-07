pipeline {

    agent any

   environment{
        PROJECT = 'impe-prod'
        PROJECT = 'impe-qa'
        PROJECT = 'impe-dev'
        ENVIRONMENT = 'prod'
        ENVIRONMENT = 'qa'
        ENVIRONMENT = 'dev'
    }

    stages{
        stage(' RUN TEST') {  
            steps {
                sh """
                echo "Running pytest test"
                pytest -v
                
                """
            }
        }        
        
         stage('BUILD IMAGE') {
              when {
                anyOf { 
			branch 'main'; branch 'qa'; branch 'dev' 
		}
            }
            steps {
                sh """
                echo " Building Docker Image"
                
                """
            }
        }
    
       
         stage(' DEPLOY ') {
              when {
                anyOf { 
			branch 'main'; branch 'qa'; branch 'dev' 
		}
            }
            steps {
                sh """
                echo " Deploying to Code Engine"
            
                  """
            }
        }
     

    }   
}
