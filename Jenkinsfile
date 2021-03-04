pipeline {

  agent any
  environment {
    //adding a comment for the commit test
    DEPLOY_CREDS = credentials('deploy-anypoint-user')
    APP_Name = 'Sandbox'
    MULE_VERSION = '4.1.3'
    BG = 'BitsInGlass'
    WORKER = 'Micro'
  }
  stages {
    stage('Build') {
      steps {
            mvn clean install
      }
    }

    stage('Test') {
      steps {
          mvn test
      }
    }

     stage('Deploy Development') {
      environment {
        ENVIRONMENT = 'Sandbox'
        APP_NAME = 'sandbox-test-db-in-clause-MK'
      }
      steps {
      
      	   echo ‘Deploying mule project due to the latest code commit…’
		   echo ‘Deploying to the configured environment….’
           mvn deploy -DmuleDeploy -Dmule.version="%MULE_VERSION%" -Danypoint.username="%DEPLOY_CREDS_USR%" -Danypoint.password="%DEPLOY_CREDS_PSW%" -Dcloudhub.app="%APP_NAME%" -Dcloudhub.environment="%ENVIRONMENT%" -Dcloudhub.bg="%BG%" -Dcloudhub.worker="%WORKER%"
      }
    }
    stage('Deploy Production') {
      environment {
        ENVIRONMENT = 'Production'
        APP_NAME = 'prod-test-db-in-clause-MK'
      }
      steps {
            mvn deploy -DmuleDeploy -Dmule.version="%MULE_VERSION%" -Danypoint.username="%DEPLOY_CREDS_USR%" -Danypoint.password="%DEPLOY_CREDS_PSW%" -Dcloudhub.app="%APP_NAME%" -Dcloudhub.environment="%ENVIRONMENT%" -Dcloudhub.bg="%BG%" -Dcloudhub.worker="%WORKER%"
      }
    }
  }

  tools {
    maven 'M3'
  }
}