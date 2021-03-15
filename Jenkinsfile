pipeline {
	agent any
	stages {
		stage("Pull Latest Image") {
			steps {
				bat "docker pull 5311072/selenium-docker"
			}
		}
		stage("Time Out Before Start Grid") {
		    steps { 
			timeout(time: 3, unit: 'SECONDS') {
			    retry(1) {
			       echo "wait for grid"
			    }   
			}
		    }    
		}
		stage("Start Grid") {
		    steps {
			bat "docker-compose up -d hub chrome firefox"
	            }
		}
		stage("Time Out Before Run Tests") {
		    steps { 
			timeout(time: 3, unit: 'SECONDS') {
			    retry(1) {
			       echo "wait for test"
			    }   
			}
		    }    
		}
		stage("Run Tests") {
		    steps {
			bat "docker-compose up book-flight-module"
		    }
		}
		stage("Finish Tests") {
		    steps { 
			timeout(time: 3, unit: 'SECONDS') {
			    retry(1) {
			       echo "shut down"
			    }   
			}
		    }    
		}
	}
	post {
	   always {
	   	 archiveArtifacts "var/jenkins_home/opt/docker/jenkins/output"
	   	 bat "docker-compose down"
	   }
    }
}
