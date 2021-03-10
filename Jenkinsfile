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
}
steps {
    withCredentials([usernamePassword(credentialsId: 'deploy-anypoint-user', passwordVariable: 'pass', usernameVariable: 'user')]) {
    	sh "mvn deploy -DmuleDeploy -Dmule.version=4.3.0 -Danypoint.username=$user -Danypoint.password=$pass -Dcloudhub.environment=${ENVIRONMENT} -Dcloudhub.bg=${BG} -Dcloudhub.worker=${WORKER} -Dworkers=1"
}
}
}
}
}
