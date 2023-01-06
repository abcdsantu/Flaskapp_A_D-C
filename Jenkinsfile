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

                zip zipFile: "flask.zip", archive: true, dir: "./"

                }
            

        }

        stage("Sonar Publish"){
            steps{
                
                    sh "ls -lrt"
                }

            
        }

        stage("Qulity Gate"){
            steps{
                 sh "scp flask.zip 192.168.145.128:~/flask_app"
                
            }
        }

        stage("Ansible Deploy"){
            steps {
                echo "${env.BUILD_NUMBER}"
                        println "${env.BUILD_NUMBER}"
                        ansiblePlaybook -vvv credentialsId: 'ansibleid', disableHostKeyChecking: true, extras: '-e BUILD_NUMBER=$BUILD_NUMBER', installation: 'ansible2', inventory: 'UAT.inv', playbook: 'flask_deploy.yaml'
            }
        }

        



    }

}
   
  