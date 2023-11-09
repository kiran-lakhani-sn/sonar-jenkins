def changeRequestNumber = "null"
def stageName = "Deploy"
def artifactname = "devops-snow-build-app.jar"
def repoName = "JenkinsDevOpsProject"
def semanticVersion = "${env.BUILD_NUMBER}.0.0"
def packageName = "devops-snow-build-pkg_${env.BUILD_NUMBER}"
def version = "${env.BUILD_NUMBER}.0"
def pkgName = "devops-snow-build-pkg_${env.BUILD_NUMBER}"

pipeline {
    agent any
    tools {
        maven "Maven"
    }
      environment {
		 SCANNER_HOME = tool 'sonarScanner'
      }
    stages {
        stage('BuildStage') {
            steps {
                echo 'Running build stage'
		snDevOpsArtifact(artifactsPayload: """{"artifacts": [{"name": "${artifactname}", "version": "1.${env.BUILD_NUMBER}","semanticVersion": "1.${env.BUILD_NUMBER}.0","repositoryName": "${repoName}"}],"branchName":"master"}""")
           	snDevOpsPackage(name: "${pkgName}-${env.BUILD_NUMBER}", artifactsPayload: """{"artifacts":[{"name": "${artifactname}", "version": "1.${env.BUILD_NUMBER}", "repositoryName": "${repoName}"}], "branchName":"master"}""")
            }
        }
        stage('TestStage') {
            steps {
                echo 'Running test stage'
	        sonarSummaries()
            }
        }
        stage('Deploy') {
            steps {
		script{
		//sh 'mvn -B package --file pom.xml'    
                echo 'Running deploy stage' 
	      //  snDevOpsSecurityResult securityResultAttributes: "{'scanner': 'Veracode','applicationName': 'PetStoreAPI-Github','securityToolId' : '15c19e6a87f1b1504a4577b8cebb3505'}"
		//snDevOpsSecurityResult securityResultAttributes: '{"scanner": "Checkmarx One", "projectName": "DemoProject", "projectId": "75acb348-c054-4ab3-807d-e17e92a923ab", "scanId": "2bb9e016-3669-488c-8341-ffa4831221f3", "securityToolId": "8bfd09b8c3253110b31ff42c05013181"}'
		//  snDevOpsSecurityResult securityResultAttributes: '{"scanner": "Checkmarx SAST", "projectId": "1076", "securityToolId": "43acfbfbc339b110b31ff42c050131c6"}'
		// veracode applicationName: "PetStoreAPI-Github", criticality: 'VeryHigh', debug: true, timeout: 20, fileNamePattern: '', pHost: '', pPassword: '', pUser: '', replacementPattern: '', sandboxName: '', scanExcludesPattern: '', scanIncludesPattern: '', scanName: "${BUILD_TAG}", uploadExcludesPattern: '', uploadIncludesPattern: 'target/DemoMavenProject*', vid: "5a57339d6779ffb76782e03df3f6e9d1", vkey: "f31d151c427a3286469a6291b14dee15e7f553e066b32c801f09014dc3282de4f51a81cd0bde7c7dd9d95de9a71a32c8a2c582158f278320ae765fe9fd232e0a", waitForScan : true
		// snDevOpsChange() 
	        snDevOpsChange changeRequestDetails: '{ "attributes": {"chg_model": "adffaa9e4370211072b7f6be5bb8f2ed"}}'
		stageName = "Deploy"
		//changeRequestNumber = snDevOpsGetChangeNumber(changeDetails: """{"stage_name":"${stageName}"}""")
		changeRequestNumber = snDevOpsGetChangeNumber(changeDetails: """{"build_number":"${env.BUILD_NUMBER}"}""")
		echo "${changeRequestNumber}"
		snDevOpsUpdateChangeInfo(changeRequestDetails: """{"close_code": "successful", "state": "3", "close_notes": "Deployment to PROD was successful test 123", "short_description": "Test description in Get_Change Step by", "priority": "1", "justification": "test justification", "description": "test description",  "cab_required": true, "comments": "This update for work notes is from jenkins file", "work_notes": "Update of change request through Update API"}""", changeRequestNumber: """${changeRequestNumber}""")
		 // snDevOpsChange()
		 // snDevOpsChange changeRequestDetails: '{ "attributes": { "short_description": "Test description", "priority": "1", "start_date": "2021-02-05 08:00:00", "end_date": "2022-04-05 08:00:00", "justification": "test justification", "description": "test description", "cab_required": true, "comments": "This update for work notes is from jenkins file", "work_notes": "test work notes", "assignment_group": "a715cd759f2002002920bde8132e7018" }, "setCloseCode": false }'
		}
            }
           
        }
    }
}
def sonarSummaries(){
 withSonarQubeEnv('sonarQube_local'){
	 sh '${SCANNER_HOME}/bin/sonar-scanner -Dsonar.projectKey=balu-sn-devops_First_repo -Dsonar.organization=First_repo -Dsonar.host.url=http://34.229.47.174/ -Dsonar.login=3dc9eb4459800df74ddf2421ec6a3ed986af3090 -Dsonar.java.binaries=target/'
	}
}
