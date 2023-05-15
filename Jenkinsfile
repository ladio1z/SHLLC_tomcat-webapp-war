
Pipeline {
	agent any

	tools {
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



node {
	def mavenName = tool name: "maven3"

	 // properties([ pipelineTriggers([pollSCM('H/5 * * * *')]) ])

	stage('1. - Clone from SCM '){
		echo "Cloning the code now"

		git branch: 'scripted', url: 'https://github.com/ladio1z/SHLLC_tomcat-webapp-war/'
	}

	stage('2. - Build from Maven '){
		echo "Building code now "
		
		sh "${mavenName}/bin/mvn clean package"
	} 

	stage('3. - Quality Code Test from Sonar ') {
		echo "Quality Code Now "

		sh "${mavenName}/bin/mvn sonar:sonar"
	}

	stage('4. - Sending Build Artifact to Nexus '){
	       echo "Moving Build Artifact to Artifactory"

	       sh "${mavenName}/bin/mvn deploy"
	}


}
