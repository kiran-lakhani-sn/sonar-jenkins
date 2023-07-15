pipeline {
    agent any
    tools {
        maven "Maven"
    }
    environment {
		SCANNER_HOME = tool 'sonarScanner'
    }
    stages {
        stage('Build') {
            steps {
                echo 'Running build stage'
            }
        }
        stage('Test') {
            steps {
                echo 'Running test stage'
            }
        }
        stage('Deploy!@$#@$@') {
            steps {
                echo 'Running deploy stage'
                //sonarSummaries()
		 snDevOpsSecurityResult securityResultAttributes: "{'scanner': 'Veracode','applicationName': 'PetStoreAPI-Github'}"
            }
           
        }
    }
}
def sonarSummaries(){
 withSonarQubeEnv('sonarQube_local'){
	 sh '${SCANNER_HOME}/bin/sonar-scanner -Dsonar.projectKey=balu-sn-devops_First_repo -Dsonar.organization=First_repo -Dsonar.host.url=http://sonarqube1.sndevops.xyz/ -Dsonar.login=3dc9eb4459800df74ddf2421ec6a3ed986af3090 -Dsonar.java.binaries=target/'
	}
}
