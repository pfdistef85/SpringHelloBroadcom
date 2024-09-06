@Library('connectall_library') _

pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building using Jenkinsfile'
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
                        GitRepoLoc: ”./",
                       // WorkspaceOid: "${env.INSIGHTS_WORKSPACE_OBJECT_ID}" ),
                        WorkspaceOid: 802910286629 )
                    


            
                       }
                   }    
         }
        stage('Create Deploy') { steps {
            script { postDeploys(
                    AutomationName: "VSIDeploys",
                    DeployId: "${env.BUILD_ID}",
                    BuildResult: "${currentBuild.currentResult}",
                    BuildFinishTime: "${String.valueOf(currentBuild.timeInMillis + currentBuild.duration)}", 
                    ConnectALL_Api_Key: "${CONNECTALL_API_KEY}",
                    ConnectALL_Api_Url: "${CONNECTALL_API_URL}",
                    Create: "false"
      }
     }
    }
  }
 } 
}
