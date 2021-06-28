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
            cd ..
            pwd
            '''
            
        }
      }
      stage('Start test app') {
         steps {
            sh '''
               sudo /usr/local/bin/docker-compose up -d
               ./scripts/test_container.sh
               '''
         }
         post {
            success {
               echo "App started successfully :)"
            }
            failure {
               echo "App failed to start :("
            }
         }
      }
      stage('Run Tests') {
         steps {
            sh ''' 
               pytest ./tests/test_sample.py
               '''
         }
      }
      stage('Stop test app') {
         steps {
            sh '''
               docker-compose down
               '''
         }
      }
   }
}
