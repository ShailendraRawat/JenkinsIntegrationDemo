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
            steps {
				echo 'Checkout code...'
				echo 'current branch name'
				echo "${env.JOB_NAME}"
				//tokens = "${env.JOB_NAME}".tokenize('/')
    			//branch = tokens[tokens.size()-1]
				//print(branch)
				checkout scm
			}
        }


		stage ('dev') {
           when { branch 'dev' }
            steps{
            sh ("this is dev branch building")
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