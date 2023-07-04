pipeline {

  agent any
  environment {
    //adding a comment for the commit test
    DEPLOY_CREDS = credentials('anypoint.credential')
    MULE_VERSION = '4.4.0'
    WORKER = "Micro"
  }
  stages {
    stage('Build') {
      steps {
            bat ‘mvn clean install’
      }
    }

    stage('Test') {
      steps {
          bat "mvn test"
      }
    }

     stage('Deploy Development') {
      environment {
        ENVIRONMENT = 'Sandbox'
        APP_NAME = 'munit-pipeline-papi'
      }
      steps {
            bat ‘mvn package -DskipTests deploy -DmuleDeploy -Dmule.version="%MULE_VERSION%" -Danypoint.username="%DEPLOY_CREDS_USR%" -Danypoint.password="%DEPLOY_CREDS_PSW%" -Dcloudhub.app="%APP_NAME%" -Dcloudhub.environment="%ENVIRONMENT%" -Dcloudhub.worker="%WORKER%"'
      }
    }
    }

}