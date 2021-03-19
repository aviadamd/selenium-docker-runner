pipeline {
	agent any
	stages {
		stage("Pull Latest Image") {	
			steps {
				bat "docker pull 5311072/selenium-docker"
			}
		}
		stage("Start Grid") {
		    steps {
		    	bat "docker-compose up -d hub chrome firefox"
	        }
		}
		stage("Run Tests") {
		    steps {
			    bat "docker-compose up book-flight-module"
		    }
		}
	}
	post {
	   always {
	   	 archiveArtifacts "**"
	   	 bat "docker-compose down"
	   }
    }
}
