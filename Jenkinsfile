pipeline{
    agent any
    environment {
        PATH = "$PATH:/usr/share/apache-maven/bin"
    }
    stages{
       stage('GetCode'){
            steps{
                git branch: 'main', changelog: false, credentialsId: 'git', poll: false, url: 'https://github.com/swamyms123/pipeline.git'
            }
       }        
       stage('Build'){
            steps{
                sh 'mvn clean package'
            }
       }
       stage('SonarQube analysis') {
            steps{
                  withSonarQubeEnv('sonarqube') { 
                  sh "mvn sonar:sonar"
					}
			}
       }
       
    }
	post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}
