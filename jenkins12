pipeline{
    agent any
        stages{
            stage("git checkout"){
            steps{
                git branch: 'main', credentialsId: 'bf72932f-d515-48d7-9249-685bb20f8616', url: 'https://github.com/harshareddy1999/hiring.git'
            }
        }
        stage("maven build"){
            steps{
                sh 'mvn clean package'
            }
        }
        stage("Tomacat deploy"){
            steps{
                sshagent(['tomcat-creditionals-cvicd']){
                    sh 'scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/"cicd tomcat hiring"/target/hiring.war centos@172.31.1.180:/opt/apache-tomcat-10.0.27/webapps' 
                    sh "ssh centos@172.31.1.180 /opt/apache-tomcat-10.0.27/bin/shutdown.sh"
                    sh "ssh centos@172.31.1.180 /opt/apache-tomcat-10.0.27/bin/startup.sh"
                }
            }
        }
        
    }
}
