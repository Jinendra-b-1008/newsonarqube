pipeline{
	agent any
	environment {
	    PATH= "/opt/maven/bin:$PATH"	
	}
	stages{
	      stage("build"){	
	        steps {
	          sh 'mvn clean deploy -Dmaven.test.skip=true'
	         }
	       }
	  	stage("test"){
                steps {
                  sh 'mvn surefire-report:report'
                 }
               }

	       stage("SonarQube analysis"){ 
		    environment{
			scannerHome = tool 'jinu-sonar-scanner'
		    }
		    steps {
			withSonarQubeEnv('jinu-sonarqube-server'){
			i	sh "${scannerHome}/bin/sonar-scanner"
			  } 
			}
		}
	}
}
