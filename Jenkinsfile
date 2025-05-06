pipeline{
    agent any
    stages{
        stage("code checkout"){
         steps{
             git branch: 'main', credentialsId: 'github', url: 'https://github.com/AYR1357/devops-r3'
         }   
        }
        stage("maven build"){
         steps{
             sh 'mvn clean package'
         }   
        }
        stage("Tomcat deploy DEV"){
         steps{
             sshagent(['tomcat-dev']) {
             // copy war file to tomcat
             sh "scp -o StrictHostKeyChecking=no target/ai-leads.war ec2-user@172.31.92.113:/opt/tomcat9/webapps"
             sh "ssh ec2-user@172.31.92.113 /opt/tomcat9/bin/shutdown.sh"
              sh "ssh ec2-user@172.31.92.113 /opt/tomcat9/bin/startup.sh"
          }
         }   
        }
    }
}
