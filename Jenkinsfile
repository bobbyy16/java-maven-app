pipeline{
    agent any
    stages{
           stage("init"){
        steps{
            script{
                echo "initilizized";
            }
        }
    }
    stage("deploy"){
        steps{
               script {
                    def dockerCmd= 'docker run -p 8080:8080 -d bobbyy16/java-maven-app:1.0'
                   sshagent(['ec2-server-key']) {
                         sh "ssh -o StrictHostKeyChecking=no ec2-user@43.205.207.73 ${dockerCmd}"
                        }
                   
                }
        }
    }
    }
}
