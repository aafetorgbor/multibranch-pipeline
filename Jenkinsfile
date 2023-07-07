pipeline {

    agent any

  parameters {
        string(name: 'PROJECT-dev', defaultValue: 'impe-dev', description: 'dev?')
        string(name: 'PROJECT-qa', defaultValue: 'impe-qa', description: 'qa?')

        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
    }

    environment{
        PROJECT = ''
        ENVIRONMENT = ''
        IMAGE_NAME = 'impe-dev-api'
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
