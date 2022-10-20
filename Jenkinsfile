pipeline{
    agent{
        docker{
            image 'maven:3.8.1-adoptopenjdk-11'
            args '-v /root/.m2:/root/.m2'
        }
    }
        options{
            skipStagesAfterUnstable()
        }
    
    stages{
        stage("Build"){
            steps{
                echo "========executing Bulild Stage========"
                sh "mvn -B -DskipTests clean package"
            }
        }
        stage("Deploy"){
            steps{
                echo "====++++executing Deploy++++===="
                sh './jenkins/scripts/deliver.sh'
            }
            post{
                always{
                    echo "====++++always++++===="
                }
                success{
                    echo "====++++Deploy executed successfully++++===="
                }
                failure{
                    echo "====++++Deploy execution failed++++===="
                }
       
            }
        }
    }
}
