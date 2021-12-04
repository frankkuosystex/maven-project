pipeline {
	agent any
	tools{
		maven 'local maven'	
	}
	stages {
		stage('Build') {
			steps {
				sh 'mvn clean package'
			}
			post {。。
				success {
					echo '開始存檔'
					archiveArtifacts artifacts: '**/target/*.war'
				}
			}
		}
		stage('Deploy to staging') {
			steps {
				build job:'deploy-to-stage'
			}
		}
		stage('Deploy to Production') {
			steps {
				timeout(time:5, units:'DAYS') {
					input message:'是否部署到生產環境'
				}
				build job:'deploy-to-production'
			}
			post {
				success {
					echo '代碼成功部署到生產環境'
				}
				failure {
					echo '部署失敗...'
				}
			}
		}	
	}
}
