pipeline {
agent any
stages {
stage(‘Build’) {
steps {
mvn clean install
}
}
stage(‘Test’) {
steps {
echo ‘Application in Testing Phase…’
mvn test
}
}
stage(‘Deploy’) {
environment {
ENVIRONMENT = 'Sandbox'
MULE_VERSION = '4.1.4'
BG = 'BitsInGlass'
ANYPOINT_CREDENTIALS = credentials(‘deploy-anypoint-user’)
APP_NAME = 'sandbox-test-db-in-clause-MK'
WORKER = 'Micro'
}
steps {
echo ‘Deploying mule project due to the latest code commit…’
echo ‘Deploying to the configured environment….’
mvn deploy -DmuleDeploy -Dmule.version="4.1.4" -Danypoint.username="ANYPOINT_CREDENTIALS_USR" -Danypoint.password="ANYPOINT_CREDENTIALS_PSW" -Dcloudhub.app=%APP_NAME" -Dcloudhub.environment="ENVIRONMENT" -Dcloudhub.bg="BG" -DworkerType="WORKER" -Dcloudhub.worker=1
}
}
}
}
