dev gv

pipeline {
    agent any
    tools{
        maven 'Maven'
        
    }
    stages {
        stage("init"){
            script{
                gv=load "dcript.groovy"
            }
        }
        stage("build jar") {
            steps {
                script{
                     gv.buildingJar()
                     sh 'mvn package'
                }
                
                
            }
        }

        stage("build image"){
            steps{
                script{
                    gv.buildingImage()
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
