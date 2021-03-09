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
APP_NAME = 'sandbox-test-db-in-clause-MK'
WORKER = 'Micro'
ANYPOINT_USERNAME_DEV = credentials('ANYPOINT_USERNAME_DEV')
ANYPOINT_PASSWORD_DEV = credentials('ANYPOINT_PASSWORD_DEV')
}
steps {
sh("mvn deploy -DmuleDeploy -Dmule.version=4.3.0 -Dusername=$ANYPOINT_USERNAME_DEV -Dpassword=$ANYPOINT_PASSWORD_DEV -Dcloudhub.environment=Sandbox -Dcloudhub.bg=BitsInGlass -DworkerType=Micro -Dworkers=1")
}
}
}
}
