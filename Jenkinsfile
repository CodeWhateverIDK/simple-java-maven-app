pipeline{
	agent any
	environment {
		SSH = credentials('ssh')
	}
	stages {
		stage('test') {
			steps {
				echo '$SSH_USR'
				echo '$SSH_PWD'
			}
		}
	}
}
