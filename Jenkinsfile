pipeline {
   agent any

   stages {
      stage('Verify Branch') {
         steps {
            echo "$GIT_BRANCH"
         }
      }
      stage('Verify hostname') {
         steps {
            sh '''hostname'''
         }
      }
      stage('Verify user') {
         steps {
            sh '''whoami'''
         }
      }
      stage('Docker Build') {
        steps {
          sh '''
            sudo docker images -a
            cd azure-vote/
            sudo docker build -t jenkins-pipeline .
            sudo docker images -a
            cd ..'''
        }
      }
   }
}
