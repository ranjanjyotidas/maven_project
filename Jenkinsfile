pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
           }
        }
        
        stage ('Deploy to Staging'){
             steps{
                    timeout(time:5, unit:'DAYS'){
                            input message:'Approve PRODUCTION Deployment?'
                    }
                    build job: 'deploy-to-staging'

                  }
                 post {
                       success {
                            echo 'CODE deployment to production.'
                          }
                       failure {
                            echo 'Daployment Failed.'
                       }

                     }
         
                       

           }
    }
}

