@Library('connectall_library') _


pipeline {
    agent any

    environment {
    INSIGHTS_API_KEY = credentials('INSIGHTS_API_KEY')
    INSIGHTS_API_URL = credentials('INSIGHTS_API_URL') 
    CONNECTALL_API_URL = credentials('CONNECTALL_API_URL')
    CONNECTALL_API_KEY = credentials('CONNECTALL_API_KEY')
    INSIGHTS_WORKSPACE_OBJECT_ID = "802910286629"
    INSIGHTS_COMPONENT_OBJECT_ID = "Mobile"
    BUILD_PATH = "REL/${currentBuild.startTimeInMillis}/${currentBuild.id}"    
    
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
                
                  
            }
        }
        stage('Create Deploy') {
            steps {
              script {
                    sh "date --date= "${currentBuild.startTimeInMillis" +%Y-%m-%dT%H:%M:%S%z"
                    postDeploys(
                        AutomationName: "VSIDeploys", 
                        DeployId: "${BUILD_PATH}", 
                        BuildStartTime: "${currentBuild.timeInMillis}",
                        BuildComponent: "liferay",
                        ConnectALL_Api_Key: "${CONNECTALL_API_KEY}",
                        ConnectALL_Api_Url: "${CONNECTALL_API_URL}",
                        Create: 'true'
                    )
              }
              // Wait for 10 seconds ensure the Deploy is created
              sleep time: 10, unit: 'SECONDS'
            }
        }
        stage('Build Current Repo') {
            steps {
              script {
                    postCommits(
                        AutomationName: "VSICommits", 
                        DeployId: "${BUILD_PATH}", 
                        GitRepoLoc: "./", 
                        PrevSuccessBuildCommit: "prod_deploy",
                        CurrentBuildCommit: "${env.GIT_COMMIT}",
                        ConnectALL_Api_Key: "${CONNECTALL_API_KEY}",
                        ConnectALL_Api_Url: "${CONNECTALL_API_URL}"
                    )
              }
            }
        }
         
 } 

}
