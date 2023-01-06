pipeline{
    agent any
    stages{
        stage("Checkout"){
            steps{
                git branch: main, url: https://github.com/abcdsantu/Flaskapp_A_D-C.git

            }

        }

        stage("Build"){
            steps{

                sh "/opt/maven/bin/mvn clean package -DskipTests=true"

                }
            

        }

        stage("Sonar Publish"){
            steps{
                withSonrQubeEnv ("sonar") {
                    sh "mvn sonar:sonar"
                }

            }
        }

        stage("Qulity Gate"){
            steps{
                script{
                    timeout(time:1, unit: "HOURS") {
                        def qg= waitForQualityGate ()
                        if (qg.status != "OK" ) {
                            error "Aborting the pipeline due to Quality Gate failed: ${qg.status}"
                        }
                    }
                    



                }
            }
        }

    }

}
   
  