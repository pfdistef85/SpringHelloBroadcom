@Library('valueops_library') _

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
        stage('Create Deploy & Commits') { 
            steps {
                script { postDeployAndCommitsToInsights(
                        ApiKey: "${env.INSIGHTS_API_KEY}",
                        ApiUrl: "${env.INSIGHTS_API_URL}",
                        BuildId: "${currentBuild.id}",
                        ComponentName : "${env.INSIGHTS_COMPONENT_OBJECT_ID}", BuildStartTime: "${currentBuild.timeInMillis}", PreviousSuccessBuildCommit: "${env.GIT_PREVIOUS_SUCCESSFUL_COMMIT}", CurrentBuildCommit: "${env.GIT_COMMIT}",
                        GitRepoLoc: ”./",
                        WorkspaceOId: "${env.INSIGHTS_WORKSPACE_OBJECT_ID}" )


            
                       }
                   }    
         }
    }
}
