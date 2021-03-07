pipeline {
agent any
stages {
stage(‘Build’) {
steps {
sh 'mvn clean install'
}
}
stage(‘Test’) {
steps {
echo ‘Application in Testing Phase…’
sh 'mvn test'
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
sh 'mvn deploy -DmuleDeploy -Dusername=${ANYPOINT_CREDENTIALS_USR} -Dpassword=${ANYPOINT_CREDENTIALS_PSW} -DworkerType=Micro -Dworkers=1'
}
}
}
}
