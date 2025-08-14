pipeline{
	agent any
	environment {
		SSH = credentials('ssh')
	}
	stages {
		stage('test') {
			steps {
				sh(echo '$SSH_USR')
				sh(echo '$SSH_PSW')
			}
		}
	}
}
