
node {
	def mavenName = tool name: "maven3"

	 // properties([ pipelineTriggers([pollSCM('* * * * *')]) ])

	stage('1. - Clone from SCM '){
		echo "Cloning the code now"

		git branch: 'scripted', url: 'https://github.com/ladio1z/SHLLC_tomcat-webapp-war/'
	}

	stage('2. - Build from Maven '){
		echo "Building code now "
		
		sh "$(mavenName)/bin/mvn clean package "
	} 

	stage('3. - Quality Code Test from Sonar ') {
		echo "Quality Code Now "

		sh "$(mavenName)/bin/mvn sonar:sonar "
	}

	stage('4. - Artifactory of Build Artifact to Nexus '){
	       echo "Moving Build Artifact to Artifactory"

	       sh "$(mavenName)/bin/mvn deploy"
	}


}
