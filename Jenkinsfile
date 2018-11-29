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
                 junit 'build/test-results/test/*.xml'
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
                   junit 'build/test-results/verify/*.xml'
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