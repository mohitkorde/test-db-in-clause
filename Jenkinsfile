pipeline {
agent any

tools { 
        maven 'Maven 3.3.9' 
        jdk 'jdk8' 
    }
    stages {
        stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                ''' 
            }
        }
stage(‘Build’) {
steps {
sh "mvn clean install"
}
}
stage(‘Test’) {
steps {
sh "mvn test"
}
}
stage(‘Deploy’) {
environment {
ENVIRONMENT = 'Sandbox'
MULE_VERSION = '4.1.3'
BG = 'BitsInGlass'
DEPLOY_CREDS = credentials('deploy-anypoint-user')
APP_NAME = 'sandbox-test-db-in-clause-MK'
WORKER = 'Micro'
}
steps {
sh '''
   echo "DEPLOY_CREDS_USR = ${DEPLOY_CREDS_USR}"
'''
sh "mvn deploy -DmuleDeploy -Dmule.version=4.3.0 -Danypoint.username=\"%DEPLOY_CREDS_USR%\" -Dpassword=Archit1127 -Dcloudhub.environment=Sandbox -Dcloudhub.bg=BitsInGlass -DworkerType=Micro -Dworkers=1"
}
}
}
}
