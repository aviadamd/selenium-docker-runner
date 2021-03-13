pipeline {
	agent any
	stages {
		stage("Start Grid") {
			steps {
				bat "docker-compose up -d hub chrome firefox"
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
			archiveArtifacts artifacts: 'output/**'
			bat "docker-compose down"
			bat "rm -rf output/"
		}
	}
}