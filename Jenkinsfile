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
		
				git branch: 'scripted', changelog: false, poll: false, url: 'https://github.com/ladio1z/SHLLC_tomcat-webapp-war/'	
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


        	stage('4 - Needing Confirmation before'){
			steps{
				echo "Needing Confimation"
                                
                          	timeout(15) {
					input message: "Please approve deployment "
				}           
			}
		}

	       
	        	
		stage('5 - Storing Artifact in Nexus'){
                        steps{
                                echo "Keep artifact in Artifactory - Nexus"
                                sh "mvn deploy"
                        }
                }
              
   }


}
