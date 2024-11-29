pipeline{
	agent any
	environment {
	    PATH= "/opt/maven/bin:$PATH"	
	}
	stages{
	      stage("build"){	
	        steps {
		  echo "-------- build started -------------"
	          sh 'mvn clean deploy -Dmaven.test.skip=true'
		  echo "--------build ended ----------------"
	         }
	       }
	  	stage("test"){
                steps {
		 echo "-------- unit test started -------------"
                  sh 'mvn surefire-report:report'
		 echo "-------- unit test ended -------------"
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
