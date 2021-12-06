pipeline {
    agent any

    tools{
        maven 'local maven'
    }

    parameters{
        string(name: 'tomcat_dev', defaultValue: '3.15.175.75', description: 'Staging Server')
        string(name: 'tomcat_prod', defaultValue: '13.58.179.83', description: 'Production Server')
    }

    triggers {
         pollSCM('* * * * *')
     }

     stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo '開始存檔...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

     stage ('Deployments'){
            parallel{
                stage ('Deploy to Staging'){
                    steps {
                        sh "scp -o StrictHostKeyChecking=no -i /home/user/.ssh/tomcat-demo.pem **/target/*.war ec2-user@${params.tomcat_dev}:/var/lib/tomcat/webapps"
                    }
                }
            }
        }
    }
}
