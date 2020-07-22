pipeline {
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