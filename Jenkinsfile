pipeline {
	agent any
	stages {
		stage("Compose Up Grid") {
			steps {
				bat "docker-compose up"
			}
		}
		stage("Compose Down Grid") {
			steps {
				bat "docker-compose down"
			}
		}
	}
}