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
				sh "mvn clean package -Dmaven.repo.local=/Users/moyv/.m2/1.6"
			}
		}
	}

	post {
		success {
      archiveArtifacts artifacts: 'monitor-parent/monitor-boot/target/*.jar', fingerprint: true
    }
	}
}
