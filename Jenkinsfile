pipeline { 

	agent any

	tools{
		maven 'maven3'
	}


	/* triggers{
		pollSCM('* * * * *')
	}
       */

	stages{

        	stage('1 - Clone from SCM'){
			steps{
				echo "Cloning from SCM "
		
				git branch: 'declarative', changelog: false, poll: false, 
				             url: 'https://github.com/ladio1z/SHLLC_tomcat-webapp-war/'	
			}
		}

        	stage('2 - Build Artifacts'){
			steps{
				echo " Building an Artifact"
				sh "mvn clean package"
			}
		}

		
		/*
        	stage('3 - Sonar'){
			steps{
				echo "Code Quality Test"
				sh "mvn sonar:sonar"
			}
		}
		*/
                

                stage('4 - Storing Artifact in Nexus'){
                        steps{
                                echo "Keep artifact in Artifactory - Nexus"
                                sh "mvn deploy"
                        }
                }


        	stage('5 - Needing Confirmation before'){
			steps{
				echo "Needing Confimation"
                                
                          	timeout(15) {
					input message: "Please approve deployment "
			        }           
			}
		}
	       
	        	
		stage('6 - Deploying Artifact to Tomcat '){
                        steps{
                                echo "Deploy an artifact to Tomcat"
                                
				deploy adapters: [tomcat9(credentialsId: 'Admin_Tomcat',
                                	path: '', url: 'http://192.168.43.212:8880/')],
	                                contextPath: null, onFailure: false, war: 'target/*.war'
                        }
                  }  
          }

}
