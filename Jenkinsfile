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
mvn deploy -DmuleDeploy -Dusername=mkorde21 -Dpassword=Mumbai10 -DworkerType=Micro -Dworkers=1
}
}
}
}
