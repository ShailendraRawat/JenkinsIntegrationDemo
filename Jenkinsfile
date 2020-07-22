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
	agent any
	stages {
		stage ('dev') {
			sh "this is dev branch building"
		}
		stage ('stage') {
			sh "this is stage branch building"
		}
		stage ('master') {
			sh "this is master branch building"
		}
	}
    always {
            echo 'always run post run'
        }
        success {
            echo 'post action as successful'
        }
        failure {
            echo 'post action as failed'
        }
}