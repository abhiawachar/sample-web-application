pipeline{

      agent any
	
	stages 
	{
        	stage ('Compile Stage') 
		{
            		steps 
			{
                		withMaven(maven : 'maven-3') 
				{
                    			sh 'mvn clean compile'
				}
            		}
        	}
        	stage ('Testing Stage') 
		{
            		steps 
			{
                	 	withMaven(maven : 'maven-3') 
				{
                    			sh 'mvn test'
                		}
            		}
        	}
        	stage('Quality Gate Status Check'){
                  steps{
                      script{
			      withSonarQubeEnv('sonarqube') { 
			      sh "mvn sonar:sonar"
                       	     	}
			      timeout(time: 1, unit: 'HOURS') {
			      def qg = waitForQualityGate()
				      if (qg.status != 'OK') {
					   error "Pipeline aborted due to quality gate failure: ${qg.status}"
				      }
                    		}
		    	    sh "mvn clean install"
		  
                 	}
               	 }  
              }	
		
            }	       	     	         
}
