pipeline {
agent any
stages {
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
MULE_VERSION = '4.1.4'
BG = 'BitsInGlass'
ANYPOINT_CREDENTIALS = credentials("deploy-anypoint-user")
APP_NAME = 'sandbox-test-db-in-clause-MK'
WORKER = 'Micro'
}
steps {
sh "mvn deploy -DmuleDeploy -Dusername=${ANYPOINT_CREDENT IALS_USR} -Dpassword=${ANYPOINT_CREDENTIALS_PSW} -DworkerType=Micro -Dworkers=1"
}
}
}
}
