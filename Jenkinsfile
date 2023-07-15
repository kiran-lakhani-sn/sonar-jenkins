pipeline {
    agent any
    tools {
        maven "Maven"
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
            }
            post{
                always{
                    snDevOpsChange()
                    }
                }   
        }
    }
}
