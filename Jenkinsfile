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
                        ComponentName: "Mobile", 
                        BuildStartTime: "${currentBuild.timeInMillis}",  
                        CurrentBuildCommit: "${env.GIT_COMMIT}",
                        GitRepoLoc: ”./",
                        WorkspaceOid: 802910286629 )
                    


            
                       }
                   }    
         }
        stage('Update Deploy Success & Finish Time in Insights') 
        { steps {
            script { postCommits(
                AutomationName: "VSICommits",
                DeployId: "${env.BUILD_ID}",
                GitRepoLoc: "./",
                PrevSuccessBuildCommit: "${env.GIT_PREVIOUS_SUCCESSFUL_COMMIT}",
                BuildIsSuccessful: currentBuild.currentResult == 'SUCCESS',
                BuildFinishTime: "${String.valueOf(currentBuild.timeInMillis + currentBuild.duration)}",
                CurrentBuildCommit: "${env.GIT_COMMIT}",
                ConnectALL_Api_Key: "${CONNECTALL_API_KEY}",
                ConnectALL_Api_Url: "${CONNECTALL_API_URL}",
                WorkspaceOid: 802910286629 )
      }
     }
    }
  }
 } 
}
