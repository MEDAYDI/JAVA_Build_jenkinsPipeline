pipeline {
    agent any
    tools{
        maven 'Maven'
        dockerTool 'docker'
    }
    stages {
        stage("build jar") {
            steps {
                script{
                     echo 'building the application ...'
                     sh 'mvn package'
                }
                
                
            }
        }

        stage("build image"){
            steps{
                script{
                    echo "building the docker image ..."
                    withCredentials([usernamePassword(credentialsId:'docker-hub-repo',passwordVariable:'PASS',usernameVariable:'USER')]){
                        sh "sudo docker build -t mohamedaydi/jenkinspipeline:1.0  . "
                        sh "echo $PASS | docker login -u ${USER} --password-stdin" 
                        sh "docker push mohamedaydi/jenkinspipeline:1.0 "
                    }
                      
                }

            }
        }
        
    }
}
