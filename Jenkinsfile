pipeline {
    agent any

    tools{
        maven 'local maven'
    }

     stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
		sh "sudo docker build . -t tomcatwebapp:${env.BUILD_ID}"
            }
        }
    }
}
