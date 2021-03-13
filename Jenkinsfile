pipeline {
	agent any
	stages {
		stage("Start Grid") {
			steps {
				bat "docker-compose up -d hub chrome firefox"
			}
		}
		stage("Wait For Tests") {
			steps { 
			  timeout(time: 3, unit: 'SECONDS') {
                retry(2) {
                   echo "wait for test"
                }   
              }
           }
		}
		stage("Run Test") {
			steps {
				bat "docker-compose up search-module book-flight-module"
			}
		}
	}
	post {
		always {
			archiveArtifacts artifacts: 'test-output/***'
			bat "docker-compose down"
			bat "rm -rf test-output/"
		}
	}
}