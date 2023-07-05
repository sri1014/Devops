pipeline{
    agent any
    stages{
        stage("Git Clone"){
            steps{
             git branch: 'main', url: 'https://github.com/sri1014/Devops.git'
            }
        }
        stage("Maven Build"){
            steps{
             sh 'mvn clean package'
            }
        }
        stage("Deploy"){
            steps{
             sshagent(['jen']) {
                 
                 sh 'scp  -o StrictHostKeyChecking=no target/chatbot.war ec2-user@172.31.2.53:/opt/tomcat9/webapps'
                 sh 'ssh ec2-user@172.31.2.53 /opt/tomcat9/bin/shutdown.sh'
                 sh 'ssh ec2-user@172.31.2.53 /opt/tomcat9/bin/startup.sh'
    
                }
            }
        }
    }
}
