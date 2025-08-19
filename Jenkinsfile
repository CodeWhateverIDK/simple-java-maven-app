pipeline {
	agent any

	environment {
		IP = '47.102.98.195'
		PORT = '20022'
		HOST = 'root'
		DIR = '/data/1.6/ic-monitor'
	}

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
		stage('Deploy') {
			steps {
				sshPublisher(publishers: [sshPublisherDesc(configName: "$IP", transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: """cd $DIR
sh bin/launch.sh restart""", execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: "$DIR", remoteDirectorySDF: false, removePrefix: 'monitor-parent/monitor-boot/target', sourceFiles: 'monitor-parent/monitor-boot/target/monitor-boot.jar')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
			}
		}
	}

	post {
		success {
      archiveArtifacts artifacts: 'monitor-parent/monitor-boot/target/*.jar', fingerprint: true
    }
		always {
			build wait: false, job: 'f1', parameters: [string(name: 'DIR', value: "$DIR"), string(name: 'IP', value: "$IP"), string(name: 'PORT', value: "$PORT"), string(name: 'HOST', value: "$HOST")]
		}
	}
}
