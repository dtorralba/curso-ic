pipeline {
    agent any
    triggers {
        pollSCM('H/2 * * * *')
    }
    stages {
        stage('Build') {
         steps {
             println 'Se empieza a ejecutar el build'
             sh "./build.sh"
         }
         post{
            always{
                println "Build ok! "
            }
         }

        }
        stage('Deploy') {
          steps {
              println 'Se empieza a ejecutar el deploy'
              sh "./deploy.sh"
          }
        }
        stage('Verify') {
           steps {
               println 'Se empieza a ejecutar el verify'
               sh "./verify.sh"
           }
           post{
               always{
                   println "Verify ok!"
                   archiveArtifacts "build/test-results/verify/*.xml"
               }
           }
        }

    }
    post {
        success {
            echo 'El job finalizó OK! :)'
        }
        failure {
            echo 'El job rompio! :('
        }
    }
}