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
    checkout scm;
    }
    }
    }
        

		stage ('dev-build') {
           when { branch 'dev' }
            steps{
            script {
              sh "this is stage branch building"
            }
            }
			
		}
        
		stage ('stage-build') {
            when { branch 'stage' }
            steps{
            sh "this is stage branch building"
            }
			
		}
		stage ('prod-build') {
            when { branch 'prod' }
             steps{
            sh "this is prod branch building"
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






