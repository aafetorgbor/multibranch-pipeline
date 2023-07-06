pipeline {

    agent any

    stages{
	    when {
                anyOf { 
			branch 'main'; branch 'qa'; branch 'dev'; branch 'PR-*'
		}
            }
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
