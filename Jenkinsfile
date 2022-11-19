pipeline{
    agent any
    environment {
        PATH = "$PATH:/usr/share/apache-maven/bin"
    }
    stages{
       stage('GetCode'){
            steps{
                git credentialsId: 'bdaac16d-a18e-4d0e-83c0-2850c1baee17', url: 'https://github.com/puneetgavri/nexus--maven-samples.git'
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
