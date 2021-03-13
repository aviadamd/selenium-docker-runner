pipeline {
	agent any
	stages {
		stage("Time Out Before Start Grid") {
		    steps { 
			timeout(time: 3, unit: 'SECONDS') {
			    retry(2) {
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
			    retry(2) {
			       echo "wait for test"
			    }   
			}
		    }    
		}
		stage("Run Tests") {
		    steps {
			bat "docker-compose up search-module book-flight-module"
		    }
		}
		stage("Finish Tests") {
		    steps { 
			timeout(time: 3, unit: 'SECONDS') {
			    retry(2) {
			       echo "shut down"
			    }   
			}
		    }    
		}
	}
	post {
	   always {
		archiveArtifacts artifacts: "output/**"
		bat "docker-compose down"
	   }
       }
}
