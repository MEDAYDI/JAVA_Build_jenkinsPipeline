pipeline {
    agent any
    tools{
        maven 'Maven'
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
                    withCredentials([usernamePasswordr(credentialsId:'docker-hub-repo',passwordVariable:'PASS',usernameVariable:'USER')]){
                        sh 'docker build -t mohamedaydi/jenkinspipeline:1.0 .'
                        sh "echo $PASS | docker login -u ${USER} --password-stdin" 
                        sh "docker push mohamedaydi/jenkinspipeline:1.0 "
                    }
                      
                }

            }
        }
        
    }
}
