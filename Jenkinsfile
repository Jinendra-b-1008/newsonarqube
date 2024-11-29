pipeline{
	agent any
	environment {
	    PATH= "/opt/maven/bin:$PATH"	
	}
	stages{
	      stage("build"){	
	        steps {
	          sh 'mvn clean deploy'
	         }
	       }
	       stage("SonarQube analysis"){ 
		    environment{
			scannerHome = tool 'jinu-sonar-scanner'
		    }
		    steps {
			withSonarQubeEnv('jinu-sonarqube-server'){
				sh "${scannerHome}/bin/sonar-scanner"
			  } 
			}
		}
	}
}
