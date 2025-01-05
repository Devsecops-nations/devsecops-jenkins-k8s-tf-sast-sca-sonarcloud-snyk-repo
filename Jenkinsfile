pipeline {
  agent any
  tools { 
        maven 'Maven_3.5.2'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		mvn clean verify sonar:sonar -Dsonar.projectKey=devsecopsguruwebapp -Dsonar.organization=devsecopsguruwebapp -Dsonar.host.url=https://sonarcloud.io -Dsonar.token=a8cb76677dab7fb1cb7473a642e7e3b1df2c13fb'
			}
    }

	stage('RunSCAAnalysisUsingSnyk') {
            steps {		
				withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
					sh 'mvn snyk:test -fn'
				}
			}
    }		
  }
}
