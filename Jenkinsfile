pipeline {
   agent any

   stages {
      stage('Verify Branch') {
         steps {
            echo "$GIT_BRANCH"
         }
      }
      stage('Docker Build') {
        steps {
          sh '''
            docker images -a
            cd azure-voting-app-redis
            docker images -a
            docker build -t jenkins-pipeline .
            cd ..'''
        }
      }
   }
}
