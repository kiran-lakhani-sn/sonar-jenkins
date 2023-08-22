pipeline {
    agent any
    tools {
        maven "Maven"
    }
    environment {
		SCANNER_HOME = tool 'sonarScanner'
    }
    stages {
        stage('Build@!') {
            steps {
                echo 'Running build stage'
            }
        }
        stage('Test&') {
            steps {
                echo 'Running test stage'
	       // sonarSummaries()
            }
        }
        stage('Deploy') {
            steps {
		//sh 'mvn -B package --file pom.xml'    
                echo 'Running deploy stage' 
	        //snDevOpsSecurityResult securityResultAttributes: "{'scanner': 'Veracode','applicationName': 'PetStoreAPI-Github','securityToolId' : 'c9db11db8764f1100801cb38dabb3531'}"
		// veracode applicationName: "PetStoreAPI-Github", criticality: 'VeryHigh', debug: true, timeout: 20, fileNamePattern: '', pHost: '', pPassword: '', pUser: '', replacementPattern: '', sandboxName: '', scanExcludesPattern: '', scanIncludesPattern: '', scanName: "${BUILD_TAG}", uploadExcludesPattern: '', uploadIncludesPattern: 'target/DemoMavenProject*', vid: "5a57339d6779ffb76782e03df3f6e9d1", vkey: "f31d151c427a3286469a6291b14dee15e7f553e066b32c801f09014dc3282de4f51a81cd0bde7c7dd9d95de9a71a32c8a2c582158f278320ae765fe9fd232e0a", waitForScan : true
		//snDevOpsChange() 
	         snDevOpsChange changeRequestDetails: '{ "attributes": {"chg_model": "e55d0bfec343101035ae3f52c1d3ae49","standard_change_template": "62d10fa1c303101035ae3f52c1d3aec1"}}'
		 //   snDevOpsChange changeRequestDetails: '{ "attributes": {"type": "standard","standard_change_template": "62d10fa1c303101035ae3f52c1d3aec1"}}'
		 // snDevOpsChange()
		 // snDevOpsChange changeRequestDetails: '{ "attributes": { "short_description": "Test description", "priority": "1", "start_date": "2021-02-05 08:00:00", "end_date": "2022-04-05 08:00:00", "justification": "test justification", "description": "test description", "cab_required": true, "comments": "This update for work notes is from jenkins file", "work_notes": "test work notes", "assignment_group": "a715cd759f2002002920bde8132e7018" }, "setCloseCode": false }'
            }
           
        }
    }
}
def sonarSummaries(){
 withSonarQubeEnv('sonarQube_local'){
	 sh '${SCANNER_HOME}/bin/sonar-scanner -Dsonar.projectKey=balu-sn-devops_First_repo -Dsonar.organization=First_repo -Dsonar.host.url=http://sonarqube1.sndevops.xyz/ -Dsonar.login=3dc9eb4459800df74ddf2421ec6a3ed986af3090 -Dsonar.java.binaries=target/'
	}
}
