pipeline {

  agent any
  environment {
    //adding a comment for the commit test
    DEPLOY_CREDS = credentials('deploy-anypoint-user')
    MULE_VERSION = '4.3.0'
    BG = "<Test>"
    WORKER = "Micro"
  }
  stages {
    stage('Build') {
      steps {
            withMaven(maven: 'maven_3.6.3')
			sh 'mvn clean compile'
      }
    }

    stage('Test') {
      steps {
            withMaven(maven: 'maven_3.6.3')
			sh 'mvn test'
      }      }
    }

     stage('Deploy Development') {
      environment {
        ENVIRONMENT = 'Sandbox'
        APP_NAME = '<test>'
      }
      steps {
            sh 'mvn -U -V -e -B -DskipTests deploy -DmuleDeploy -Dmule.version="%MULE_VERSION%" -Danypoint.username="%DEPLOY_CREDS_USR%" -Danypoint.password="%DEPLOY_CREDS_PSW%" -Dcloudhub.app="%APP_NAME%" -Dcloudhub.environment="%ENVIRONMENT%" -Dcloudhub.bg="%BG%" -Dcloudhub.worker="%WORKER%"'
      }
    }
    
		}	

}