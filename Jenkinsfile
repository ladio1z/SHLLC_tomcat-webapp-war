Pipeline { 

tools{
		maven 'maven3'
	}

	triggers{
		pollSCM('* * * * *')
	}

   stages{
		stage('1 - Clone from SCM'){
			steps{
				echo "Cloning from SCM "
				
				git branch: 'declarative', changelog: false, poll: false, url: 'https://github.com/ladio1z/SHLLC_tomcat-webapp-war/'
			}
		}
   }

}