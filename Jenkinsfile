
Pipeline {
	agent any

	tools{
		maven 'maven3'
	}
	
	triggers {
		pollSCM('* * * * *')
	}

   stages{
		stage('1 - Clone from SCM'){
			steps{
				echo "Cloning from SCM "
				
				git branch: 'declarative', changelog: false, poll: false, url: 'https://github.com/ladio1z/SHLLC_tomcat-webapp-war/'
			}
		}

		stage('1 - Build Artifacts'){
			steps{
				echo " Building an Artifact"
				sh "mvn clean package"
			}
		}

		stage('3 - Sonar'){
			steps{
				echo "Code Quality Test"
				sh "mvn sonar:sonar"
			}
		}

		stage('4 - Storing Artifact in Nexus'){
			steps{
				ehco "Keep artifact in Artifactory - Nexus"
				sh "mvn deploy"
			}
		}

   }
}