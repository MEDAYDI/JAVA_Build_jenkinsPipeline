pipeline {
    agent {
        docker {
            image 'docker:19.03.12'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    tools{
        maven 'Maven'
        docker 'docker'
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
                        sh "docker build -t mohamedaydi/jenkinspipeline:1.0  . "
                        sh "echo $PASS | docker login -u ${USER} --password-stdin" 
                        sh "docker push mohamedaydi/jenkinspipeline:1.0 "
                    }
                      
                }

            }
        }
        
    }
}
