pipeline {
    agent any
     tools {
        maven 'Maven' 
        }
    stages {
        stage("Test"){
            steps{
                // mvn test
                sh "mvn test"
               // slackSend channel: 'youtubejenkins', message: 'Job Started'
                
            }
            
        }
        stage("Build"){
            steps{
                sh "mvn package"
                
            }
            
        }
        stage("Deploy on Test"){
            steps{
                //deploy on container -> plugin
                //deploy adapters: [tomcat9(credentialsId: 'tomcat9details', path: '', url: 'http://43.205.143.146:8086')], contextPath: '/root/apache-tomcat-9.0.73/webapps/app/', war: '**/*.war'
                  deploy adapters: [tomcat9(credentialsId: 'saikrishna', path: '', url: 'http://43.205.143.146:8086')], contextPath: '/root/apache-tomcat-9.0.73/webapps/app', war: '**/*.war'
              }
            
        }
        stage("Deploy on Prod"){
             input {
                message "Should we continue?"
                ok "Yes we Should"
             }
            
            steps{
                // deploy on container -> plugin
                 deploy adapters: [tomcat9(credentialsId: 'saikrishna', path: '', url: 'http://13.235.246.101:8086')], contextPath: '/app', war: '**/*.war'

             }
         }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
             //slackSend channel: 'youtubejenkins', message: 'Success'
        }
        failure{
            echo "========pipeline execution failed========"
            // slackSend channel: 'youtubejenkins', message: 'Job Failed'
        }
  }
}
