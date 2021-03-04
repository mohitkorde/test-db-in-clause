pipeline {
agent any
stages {
stage(‘Build Application’) {
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
stage(‘Deploy CloudHub’) {
environment {
ANYPOINT_CREDENTIALS = credentials(‘deploy-anypoint-user’)
}
steps {
echo ‘Deploying mule project due to the latest code commit…’
echo ‘Deploying to the configured environment….’
mvn package deploy -DmuleDeploy -Dusername=${ANYPOINT_CREDENTIALS_USR} -Dpassword=${ANYPOINT_CREDENTIALS_PSW} -DworkerType=Micro -Dworkers=1
}
}
}
}
