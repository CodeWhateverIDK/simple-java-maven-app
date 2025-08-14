pipeline{
	agent any
	environment {
		SSH = credentials('ssh')
	}
	stages {
		stage('test') {
			step {
				echo '$SSH_USR'
				echo '$SSH_PWD'
			}
		}
	}
}
