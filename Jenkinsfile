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
		stage("Run Test") {
			steps {
				bat "docker-compose up search-module book-flight-module"
			}
		}
	}
	post {
		always {
			archiveArtifacts artifacts: 'output/**'
			sh "docker-compose down"
			sh "sudo rm -rf output/"
		}
	}
}