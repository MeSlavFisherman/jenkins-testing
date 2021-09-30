
pipeline {
  agent any
  parameters {
      string(name:  'VERSION', defaultValue: '', description: 'version to deploy on prod')
      choice(name:  'VERSION2', choices: ['1.1','1.2','1.3'], description: '')
      booleanParam(name:  'executeTests', defaultValue: true, description: '')
  }
  environment {
      NEW_VERSION = '1.1.0'
      SERVER_CREDENTIALS = credentials('server-creds')
  }
  stages {
    
    stage("build") {
      /* when {
          expression {
              BRANCH_NAME == 'dev' || CODE_CHANGES == true
          }
      } */
      steps {
         echo 'building the app...'
         echo "Building version ${NEW_VERSION}" //double quotes for env variables
         echo "deploying verion ${params.VERSION2}"
      }
    }
    
    stage("test") {
      when {
          expression {
              BRANCH_NAME == 'dev' || BRANCH_NAME == 'master'
          }
      }
      steps {
         echo 'testing the app...'
      }
    }
    
    stage("deploy") {
      when {
        expression {
          params.executeTests == true
        }
      }
      steps {
         echo 'deploying the app..'
         echo "deploying with ${SERVER_CREDENTIALS}"
         echo "deploying verion ${params.VERSION}"
      }
    }
  }
/*   post {
    always {
      
    }
    success {
    
    }
    
    failure {
      
    }
  } */
}
