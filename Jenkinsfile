@Library('connectall_library') _


pipeline {
    agent any

    environment {
    INSIGHTS_API_KEY = credentials('INSIGHTS_API_KEY')
    INSIGHTS_API_URL = credentials('INSIGHTS_API_URL')    
    INSIGHTS_WORKSPACE_OBJECT_ID = "802910286629"
    INSIGHTS_COMPONENT_OBJECT_ID = "Mobile"
    BUILD_PATH = 'REL\\'"${currentBuild.startTimeInMillis}"'\\'"${currentBuild.id}"  
    
}

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                echo "$BUILD_PATH"
               
                
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying..'
                
                
            }
        }
        stage('Create Deploy & Commits in Insights') { 
            steps {
                script { postDeployAndCommitsToInsights(
                        ApiKey: "${env.INSIGHTS_API_KEY}",
                        ApiUrl: "${env.INSIGHTS_API_URL}",
                        WorkspaceOid: "${env.INSIGHTS_WORKSPACE_OBJECT_ID}",
                        CurrentBuildCommit: "${env.GIT_COMMIT}",
                        BuildId: "${BUILD_PATH}",
                        ComponentName: "${env.INSIGHTS_COMPONENT_OBJECT_ID}", 
                        BuildStartTime: "${currentBuild.timeInMillis}",  
                        GitRepoLoc: "./" )
                    


            
                       }
                   }    
         }
        
  }
 } 
