@Library('connectall_library') _


pipeline {
    agent any

    environment {
    INSIGHTS_API_KEY = credentials('INSIGHTS_API_KEY')
    INSIGHTS_API_URL = credentials('INSIGHTS_API_URL')    
    INSIGHTS_WORKSPACE_OBJECT_ID = "802910286629"
    API_WORKSPACE_OID = "802910286629"
    INSIGHTS_COMPONENT_OBJECT_ID = "Mobile"
    
}

    stages {
        stage('Build') {
            steps {
                echo 'Building using Jenkinsfile'
                echo 'Insights API Key ${INSIGHTS_API_KEY}'
                echo 'Insights API URL ${INSIGHTS_API_URL}'
                
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
        stage('Create Deploy & Commits in Insights') { 
            steps {
                script { postDeployAndCommitsToInsights(
                        ApiKey: "${env.INSIGHTS_API_KEY}",
                        ApiUrl: "${env.INSIGHTS_API_URL}",
                        BuildId: "${currentBuild.id}",
                        ComponentName: "${env.INSIGHTS_COMPONENT_OBJECT_ID}", 
                        BuildStartTime: "${currentBuild.timeInMillis}",  
                        CurrentBuildCommit: "${env.GIT_COMMIT}",
                        GitRepoLoc: "./",
                        WorkspaceOid: "${env.INSIGHTS_WORKSPACE_OBJECT_ID}" )
                    


            
                       }
                   }    
         }
        stage('Update Deploy Success & Finish Time in Insights') { 
            steps {
            script { updateDeployToInsights(

                ApiKey: "${env.INSIGHTS_API_KEY}",
                ApiUrl: "${env.INSIGHTS_API_URL}",
                BuildId: "${currentBuild.id}",
                GitRepoLoc: "./",
                BuildFinishTime: "${String.valueOf(currentBuild.timeInMillis + currentBuild.duration)}",
                BuildIsSuccessful: currentBuild.currentResult == 'SUCCESS',
                WorkspaceOid: "${env.INSIGHTS_WORKSPACE_OBJECT_ID}" )
      }
     }
    }
  }
 } 

