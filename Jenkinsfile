pipeline {

    agent any
    
    
      stages{
        stage("Checkout Code") {
            steps {
                checkout scm
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
               branch 'dev';
               branch 'qa';
               branch 'main'
           }
            steps {
                sh """
                echo " Deploying to Code Engine"
            
                  """
            }
        }
     

    }   
}
