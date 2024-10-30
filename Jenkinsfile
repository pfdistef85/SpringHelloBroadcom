@Library('connectall_library') _


pipeline {
    agent any

    environment {
    INSIGHTS_API_KEY = credentials('INSIGHTS_API_KEY')
    INSIGHTS_API_URL = credentials('INSIGHTS_API_URL') 
    CONNECTALL_API_URL = credential('CONNECTALL_API_URL')
    CONNECTALL_API_KEY = credential('CONNECTALL_API_KEY')
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
                
                script {
                        BuildPath = "Rel/${env.GIT_COMMIT}/${currentBuild.id}"
                        }    
            }
        }
        stage('Create Deploy') {
            steps {
              script {
                    sh "date --date='@1721865551' +%Y-%m-%dT%H:%M:%S%z"
                    postDeploys(
                        AutomationName: "VSIDeploys", 
                        DeployId: "${BuildPathenv.BUILD_ID}", 
                        BuildStartTime: "${currentBuild.timeInMillis}",
                        BuildComponent: "connectall", 
                        ConnectALL_Api_Key: "${CONNECTALL_API_KEY}",
                        ConnectALL_Api_Url: "${CONNECTALL_API_URL}",
                        Create: 'true'
                    )
              }
              // Wait for 10 seconds ensure the Deploy is created
              sleep time: 10, unit: 'SECONDS'
            }
        }
        stage('Update Deploy Success & Finish Time in Insights') { 
            steps {
            script { updateDeployToInsights(

                ApiKey: "${env.INSIGHTS_API_KEY}",
                ApiUrl: "${env.INSIGHTS_API_URL}",
                WorkspaceOid: "${env.INSIGHTS_WORKSPACE_OBJECT_ID}",
                CurrentBuildCommit: "${env.GIT_COMMIT}",
                BuildId: "${BuildPath}",
                BuildFinishTime: "${String.valueOf(currentBuild.timeInMillis + currentBuild.duration)}",
                BuildIsSuccessful: currentBuild.currentResult == 'SUCCESS' )
      }
     }
    }
  }
 } 

