pipeline{
    agent any
    stages{
        stage("Checkout"){
            steps{
                git branch: "main", url: "https://github.com/abcdsantu/Flaskapp_A_D-C.git"

            }

        }

        stage("Build with ZIP"){
            steps{

                zip zipFile: "flskapp_BUILD_NUMBER.zip", archive: true, dir: "./"

                }
            

        }

        stage("Sonar Publish"){
            steps{
                
                    sh "ls -lrt"
                }

            
        }

        stage("Qulity Gate"){
            steps{
                 sh "docker images"
                
            }
        }

        stage("Ansible Deploy"){
            steps {
                echo "${env.BUILD_NUMBER}"
                        println "${env.BUILD_NUMBER}"
                        ansiblePlaybook credentialsId: 'ansibleid', disableHostKeyChecking: true, extras: '-e BUILD_NUMBER=$BUILD_NUMBER', installation: 'ansible2', inventory: 'UAT.inv', playbook: 'flask_deploy.yaml'
            }
        }

        



    }

}
   
  