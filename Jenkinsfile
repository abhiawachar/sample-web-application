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
        	stage('Quality Gate Status Check')
		{
                  steps{
                      withSonarQubeEnv(credentialsId: 'sonarqubetoken') 
			  {
				    sh 'mvn clean install'
			  }
               	 	}  
               }	
		
           }	       	     	         
}
