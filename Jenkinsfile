pipeline {
	agent any

	options {
		// Job timeout
		timeout(time: 5, unit: 'MINUTES')
		// Add timestamps to console output
		timestamps()
		// Disable multiple builds at a time for same branch/job
		disableConcurrentBuilds()
		// Only keep 60 builds
		buildDiscarder(logRotator(numToKeepStr: '60'))
	}
	stages {
    stage('checkout'){
        steps{
            script{
    context="continuous-integration/jenkins/";
    context += isPRMergeBuild()?"pr-merge/checkout":"branch/checkout";
    checkout scm;
    setBuildStatus ("${context}", 'Checking out completed', 'SUCCESS');
    }
        }
    }
        


		stage ('dev') {
           when { branch 'dev' }
            steps{
            sh '''
            echo "hello world"
            
            '''
            }
			
		}
		stage ('stage') {
            when { branch 'stage' }
            steps{
            sh "this is stage branch building"
            }
			
		}
		stage ('master') {
            when { branch 'master' }
             steps{
            sh "this is master branch building"
            }
			
		}
	}
    post {
        always {
            cleanWs()
        }
        success {
            echo 'post action as successful'
        }
        failure {
            echo 'post action as failed'
        }



    }
    
}

def isPRMergeBuild() {
    return (env.BRANCH_NAME ==~ /^PR-\d+$/)
}


void setBuildStatus(context, message, state) {
  step([
      $class: "GitHubCommitStatusSetter",
      contextSource: [$class: "ManuallyEnteredCommitContextSource", context: context],
      errorHandlers: [[$class: "ChangingBuildStatusErrorHandler", result: "UNSTABLE"]],
      reposSource: [$class: "ManuallyEnteredRepositorySource", url: "https://github.com/${getRepoSlug()}"],
      statusResultSource: [ $class: "ConditionalStatusResultSource", results: [[$class: "AnyBuildResult", message: message, state: state]] ]
  ]);
}


def getRepoSlug() {
    tokens = "${env.JOB_NAME}".tokenize('/')
    org = tokens[tokens.size()-3]
    repo = tokens[tokens.size()-2]
    return "${org}/${repo}"
}

def getBranch() {
    tokens = "${env.JOB_NAME}".tokenize('/')
    branch = tokens[tokens.size()-1]
    return "${branch}"
}

