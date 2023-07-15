pipeline {
    agent any
    tools {
        maven "Maven"
    }
    environment {
		SCANNER_HOME = tool 'sonarScanner'
    }
    stages {
        stage('Build!@$#@$@') {
            steps {
                echo 'Running build stage'
            }
        }
        stage('Test') {
            steps {
                echo 'Running test stage'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Running deploy stage'
                //sonarSummaries()
		 //snDevOpsSecurityResult securityResultAttributes: "{'scanner': 'Veracode','applicationName': 'PetStoreAPI-Github'}"
		 veracode applicationName: "PetStoreAPI-Github", criticality: 'VeryHigh', debug: true, timeout: 20, fileNamePattern: '', pHost: '', pPassword: '', pUser: '', replacementPattern: '', sandboxName: '', scanExcludesPattern: '', scanIncludesPattern: '', scanName: "${BUILD_TAG}", uploadExcludesPattern: '', uploadIncludesPattern: 'target/DevOps-Test-1.39.0-SNAPSHOT.jar', vid: "5a57339d6779ffb76782e03df3f6e9d1", vkey: "f31d151c427a3286469a6291b14dee15e7f553e066b32c801f09014dc3282de4f51a81cd0bde7c7dd9d95de9a71a32c8a2c582158f278320ae765fe9fd232e0a", waitForScan : 'true'
            }
           
        }
    }
}
def sonarSummaries(){
 withSonarQubeEnv('sonarQube_local'){
	 sh '${SCANNER_HOME}/bin/sonar-scanner -Dsonar.projectKey=balu-sn-devops_First_repo -Dsonar.organization=First_repo -Dsonar.host.url=http://sonarqube1.sndevops.xyz/ -Dsonar.login=3dc9eb4459800df74ddf2421ec6a3ed986af3090 -Dsonar.java.binaries=target/'
	}
}
