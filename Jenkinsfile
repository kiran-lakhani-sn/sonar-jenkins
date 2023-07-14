def artifactname = "devops-snow-build-app.jar"
def repoName = "JenkinsDevOpsProject"
def pipelineName = "SunilPipelines/Sunil-Scripted-Pipeline-Sonar"
def semanticVersion = "${env.BUILD_NUMBER}.0.0"
def packageName = "devops-snow-build-prasad_pkg_${env.BUILD_NUMBER}"
def version = "${env.BUILD_NUMBER}.0"
def pkgName = "devops-snow-build-prasad_pkg_${env.BUILD_NUMBER}"

pipeline {
  agent any
  tools {
       maven 'Maven'
   }
   environment {
	 SCANNER_HOME = tool 'sonarScanner'
	}  
  stages {
       stage('Build') {
           steps {
              
              sh 'mvn -B -DskipTests clean compile'

           }
       }
       stage('Test') {
           steps {
              
              sh 'mvn test'
	    
	      sonarSummaries()
              snDevOpsArtifact(artifactsPayload: """{"artifacts": [{"name": "${artifactname}", "version": "1.${env.BUILD_NUMBER}","semanticVersion": "1.${env.BUILD_NUMBER}.0","repositoryName": "${repoName}"}],"branchName":"master"}""")
              snDevOpsPackage(name: "${pkgName}-${env.BUILD_NUMBER}", artifactsPayload: """{"artifacts":[{"name": "${artifactname}", "version": "1.${env.BUILD_NUMBER}", "repositoryName": "${repoName}"}], "branchName":"master"}""")
           }
           post {
             always {
                junit "**/target/surefire-reports/*.xml"
             }
           }
       }
      stage('Deploy') {
                 steps {
                    

		    snDevOpsChange(ignoreErrors:false)
                    
                 }
      }


 }
 
}

def sonarSummaries() {

  // withSonarQubeEnv('SonarCloud') {
       //sh '${SCANNER_HOME}/bin/sonar-scanner -Dproject.settings=${SCANNER_HOME}/conf/qa-sonar-scanner-cloud.properties'
     //  sh '${SCANNER_HOME}/bin/sonar-scanner -Dsonar.projectKey=sunilyerubandi_DemoMavenProject -Dsonar.organization=sunilyerubandi -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=8f73ecadbe478e324214c741569315dddfa01ee5 -Dsonar.java.binaries=target/ -Dsonar.branch.name=master'
   
	//}
	
   withSonarQubeEnv('sonarQube_local') {

       	sh '${SCANNER_HOME}/bin/sonar-scanner -Dproject.settings=${SCANNER_HOME}/conf/qa-sonar-scanner.properties'
   		// sh '${SCANNER_HOME}/bin/sonar-scanner -Dproject.settings=${SCANNER_HOME}/conf/sonar-scanner.properties'
	}
	
} // end of def sonarsummaries
