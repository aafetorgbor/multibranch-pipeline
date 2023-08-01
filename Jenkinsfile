pipeline {

    agent any

    environment{
        //BRANCH_NAME_MAIN   = 'main'
        //BRANCH_NAME_QA     = 'qa'
        //BRANCH_NAME_DEV    = 'dev'
        PROJECT            = 'project'
        PROJECT_PROD       = 'impe-prod'
        PROJECT_QA         = 'impe-qa'
        PROJECT_DEV        = 'impe-dev'
        ENVIRONMENT        = 'environment'
      //  ENVIRONMENT_QA     = 'qa'
       // ENVIRONMENT_DEV    = 'dev'
        IMAGE_NAME         = 'image-name'
       // IMAGE_NAME_QA      = 'impe-qa-api'
        //IMAGE_NAME_DEV     = 'impe-dev-api'
    }
    
      stages{
        stage(' RUN TEST') {  
            steps {
                sh """
                echo "Running pytest test"
                pytest -v
                printenv
                
                """
            }
        }
        
        
         stage('BUILD IMAGE') {
           
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'multibranch-github-PAT', url: 'https://github.com/aafetorgbor/JavaScript-unittest-jest.git']]])
                dir("impe_config/${ENVIRONMENT}"){
                    stash includes: "enabled_tools.yaml", name: "enabled_tools"
                }

                checkout([$class: 'GitSCM', branches: [[name: '*/${BRANCH_NAME}']], extensions: [], userRemoteConfigs: [[credentialsId: 'multibranch-github-PAT', url: 'https://github.com/aafetorgbor/multibranch-pipeline.git']]])
                 dir("src/config"){
                    unstash "enabled_tools"
                 }

                script{
                    
                    if( env.BRANCH_NAME == 'main' &&  env.PROJECT_PROD == 'impe-prod'){
                        
                        withEnv(["PROJECT=impe-prod", 
                                "ENVIRONMENT=prod ", 
                                "IMAGE_NAME=impe-prod-api"] ){
                        
                        sh """
                        echo " Building Docker image and publishing to PROD"
                        echo " PROJECT = ${PROJECT}"
                        echo " ENVIRONMENT = ${ENVIRONMENT}"
                        echo " IMAGE_NAME = ${IMAGE_NAME}"
            
                        """
                        }  
                    }else if (env.BRANCH_NAME == 'qa' &&  env.PROJECT_QA == 'impe-qa') {
                        
                         withEnv(["PROJECT=impe-qa",
                                 "ENVIRONMENT=QA ", 
                                 "IMAGE_NAME=impe-qa-api"]){
                        
                        sh """
                        echo " Building Docker image and publishing to QA"
                        echo " PROJECT = ${PROJECT}"
                        echo " ENVIRONMENT = ${ENVIRONMENT}"
                        echo " IMAGE_NAME = ${IMAGE_NAME}"
            
                        """
                        }  
                    }else if (env.BRANCH_NAME == 'dev' &&  env.PROJECT_DEV == 'impe-dev') {
                        
                         withEnv(["PROJECT=impe-dev",
                         "ENVIRONMENT=dev ", 
                         "IMAGE_NAME=impe-dev-api"]){
                        
                        sh """
                        echo " Building Docker image and publishing to DEV"
                        echo " PROJECT = ${PROJECT}"
                        echo " ENVIRONMENT = ${ENVIRONMENT}"
                        echo " IMAGE_NAME = ${IMAGE_NAME}"
            
                        """
                        }  
                    }else{
                        sh """
                        echo " BRANCH_NAME is != prod, qa, or dev"
                      
                         """
                    }   
                   
                }                
            }
        }
    
       
         stage(' DEPLOY ') {
            steps {
                
                script{
                    
                    if( env.BRANCH_NAME == 'main' &&  env.PROJECT_PROD == 'impe-prod'){
                        
                        withEnv(["PROJECT=impe-prod",
                                 "ENVIRONMENT=prod ", 
                                 "IMAGE_NAME=impe-prod-api"] ){
                        
                        sh """
                        echo " Deploying to Code Engine PROD"
                        echo " PROJECT = ${PROJECT}"
                        echo " ENVIRONMENT = ${ENVIRONMENT}"
                        echo " IMAGE_NAME = ${IMAGE_NAME}"
            
                        """
                        }  
                    }else if (env.BRANCH_NAME == 'qa' &&  env.PROJECT_QA == 'impe-qa') {
                        
                         withEnv(["PROJECT=impe-qa",
                                 "ENVIRONMENT=QA ", 
                                 "IMAGE_NAME=impe-qa-api"]){
                        
                        sh """
                        echo " Deploying to Code Engine QA"
                        echo " PROJECT = ${PROJECT}"
                        echo " ENVIRONMENT = ${ENVIRONMENT}"
                        echo " IMAGE_NAME = ${IMAGE_NAME}"
            
                        """
                        }  
                    }else if (env.BRANCH_NAME == 'dev' &&  env.PROJECT_DEV == 'impe-dev') {
                        
                         withEnv(["PROJECT=impe-dev",
                                  "ENVIRONMENT=dev ",
                                  "IMAGE_NAME=impe-dev-api"]){
                        
                        sh """
                        echo " Deploying to Code Engine DEV"
                        echo " PROJECT = ${PROJECT}"
                        echo " ENVIRONMENT = ${ENVIRONMENT}"
                        echo " IMAGE_NAME = ${IMAGE_NAME}"
            
                        """
                        }  
                    }else{
                        sh """
                        echo " BRANCH_NAME is != prod, qa, or dev"
                                 
                         """
                    }   
                    
                }
                
            }
        }    

    }   
}
