pipeline {

    agent any
    
    
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
            steps {
                sh """
                echo " Building Docker Image"
                
                """
            }
        }
    
       
         stage(' DEPLOY ') {
            steps {
                sh """
                echo " Deploying to Code Engine"
            
                  """
            }
        }
     

    }   
}
