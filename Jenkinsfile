@Library('connectall_library') _


pipeline {
    agent any

    environment {
    INSIGHTS_API_KEY = credentials('INSIGHTS_API_KEY')
    INSIGHTS_API_URL = credentials('INSIGHTS_API_URL')    
    INSIGHTS_WORKSPACE_OBJECT_ID = "802910286629"
    INSIGHTS_COMPONENT_OBJECT_ID = "Mobile"
    
}

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
               
                
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
                writeFile(file: "Rel/${env.GIT_COMMIT}/${currentBuild.id}", text: "áéíóú", encoding: "UTF-8")
    
            }
        }
        stage('Create Deploy & Commits in Insights') { 
            steps {
                script { postDeployAndCommitsToInsights(
                        ApiKey: "${env.INSIGHTS_API_KEY}",
                        ApiUrl: "${env.INSIGHTS_API_URL}",
                        WorkspaceOid: "${env.INSIGHTS_WORKSPACE_OBJECT_ID}",
                        CurrentBuildCommit: "${env.GIT_COMMIT}",
                        BuildId: "${currentBuild.id}",
                        ComponentName: "${env.INSIGHTS_COMPONENT_OBJECT_ID}", 
                        BuildStartTime: "${currentBuild.timeInMillis}",  
                        GitRepoLoc: "./" )
                    


            
                       }
                   }    
         }
        stage('Update Deploy Success & Finish Time in Insights') { 
            steps {
            script { updateDeployToInsights(

                ApiKey: "${env.INSIGHTS_API_KEY}",
                ApiUrl: "${env.INSIGHTS_API_URL}",
                WorkspaceOid: "${env.INSIGHTS_WORKSPACE_OBJECT_ID}",
                CurrentBuildCommit: "${env.GIT_COMMIT}",
                BuildId: "${currentBuild.id}",
                BuildFinishTime: "${String.valueOf(currentBuild.timeInMillis + currentBuild.duration)}",
                BuildIsSuccessful: currentBuild.currentResult == 'SUCCESS' )
      }
     }
    }
  }
 } 

