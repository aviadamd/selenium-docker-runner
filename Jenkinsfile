pipeline {
	agent any
	stages {
		stage("Pull Latest Image") {
			timeout(time: 3, unit: 'SECONDS')	
			steps {
				bat "docker pull 5311072/selenium-docker"
			}
		}
		stage("Start Grid") {
			timeout(time: 3, unit: 'SECONDS')
		    steps {
		    	bat "docker-compose up -d hub chrome firefox"
	        }
		}
		stage("Run Tests") {
			timeout(time: 3, unit: 'SECONDS')
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
