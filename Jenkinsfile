pipeline{
    agent any
    tools{
        maven 'Maven-3.8.6'
    }
    stages{
        stage("build jar"){
            steps{
                script {
                    echo "building the application"
                    sh 'mvn package'
                }
            }
        }
        stage("build iamge"){
            steps{
                script {
                    echo "building the docker image"

                    withCredentials([usernamePassword(
                    CredentialsId: 'docker-hub-repo',
                    passwordVariable: 'PASS',
                    usernameVariable: 'USER'
                    )]) {
                        sh 'docker build -t bobbyy16/java-maven-app:1.2 .'
                        sh "echo $PASS | docker login -u $USER --password-stdin"
                        sh 'docker push bobbyy16/java-maven-app:1.2'
                    }
                }
            }
        }
        stage("deploy"){
            steps{
                script {
                    echo "deploying the application"
                }
            }
        }
    }
}
