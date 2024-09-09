@Library('connectall_library') _
environment {
    ApiKey = credentials("INSIGHTS_API_KEY")
    ApiURL = credentials("INSIGHTS_API_URL")    
}

pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building using Jenkinsfile'
                echo "API Key is "
                echo "API URL is ${ApiURL}"
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
                        $ApiKey,
                        $ApiUrl,
                        BuildId: "${currentBuild.id}",
                        ComponentName: "Mobile", 
                        BuildStartTime: "${currentBuild.timeInMillis}",  
                        CurrentBuildCommit: "${env.GIT_COMMIT}",
                        GitRepoLoc: "./",
                        WorkspaceOid: 802910286629 )
                    


            
                       }
                   }    
         }
        stage('Update Deploy Success & Finish Time in Insights') { 
            steps {
            script { postCommits(
                AutomationName: "VSICommits",
                DeployId: "${env.BUILD_ID}",
                GitRepoLoc: "./",
                PrevSuccessBuildCommit: "${env.GIT_PREVIOUS_SUCCESSFUL_COMMIT}",
                BuildIsSuccessful: currentBuild.currentResult == 'SUCCESS',
                BuildFinishTime: "${String.valueOf(currentBuild.timeInMillis + currentBuild.duration)}",
                CurrentBuildCommit: "${env.GIT_COMMIT}",
                ApiKey,
                ApiUrl,
                WorkspaceOid: 802910286629 )
      }
     }
    }
  }
 } 

