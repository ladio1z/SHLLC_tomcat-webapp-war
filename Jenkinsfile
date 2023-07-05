
node {
	def mavenName = tool name: "maven3"

	 // properties([ pipelineTriggers([pollSCM('H/5 * * * *')]) ])

	stage('1st. - Clone from SCM '){
		
		echo "Cloning the code now"

		git branch: 'scripted', changelog: false, poll: false, url: 'https://github.com/ladio1z/SHLLC_tomcat-webapp-war/'	
	}


	stage('2nd. - Build from Maven '){
		
		echo "Building code now "
		
		sh "${mavenName}/bin/mvn clean package"
	} 


/*
	stage('3rd. - Quality Code Test from Sonar ') {
		
		echo "Quality Code Now "

		sh "${mavenName}/bin/mvn sonar:sonar"
	}
*/

	stage('4th. - Sending Build Artifact to Nexus '){

               echo "Moving Build Artifact to Artifactory"

               sh "${mavenName}/bin/mvn deploy"
        }


	stage('5th. - Needing Confirmation ')	{
              
	      echo "Needing Confirmation to Integration Nexus"
           
	      timeout(10) {
                input message: "Please Confirm to Integration Nexus"
               }

        }
	
	stage('6th. - Deploying the Build Artifact to Tomcat '){
	       
	       echo "Deploying Artifacts to Tomcat"
              
	      deploy adapters: [tomcat9(credentialsId: 'Admin_Tomcat', 
	                        path: '', url: 'http://192.168.43.212:8880/')],
				contextPath: null, onFailure: false, war: 'target/*.war'
	      
	}


}
