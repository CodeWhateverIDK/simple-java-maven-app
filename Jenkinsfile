pipeline {
	agent any
	tools {
  	maven 'Maven3.9.11'
		jdk 'JDK8' 
  }
	stages {
		stage('Checkout') {
			steps {
				git branch: '1.6', credentialsId: 'lxl', url: 'https://gitee.com/szyh/ic-monitor.git'
			}
		}
		stage('Build') {
			steps {
				sh "mvn clean package -Dmaven.test.skip=true"
			}
		}
	}

	post {
		success {
      archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
    }
	}
}
