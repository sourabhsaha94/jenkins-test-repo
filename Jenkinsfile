pipeline {
	agent any
	stages {
		stage('Build') {
			steps {
				sh 'echo "Hello World"'
				sh '''
					echo "Multiline shell steps works too"
					ls -lah
				'''
            		}
        	}
		stage('Deploy'){
			steps {
				retry(3) {
					sh 'echo "This is deploy stage"'
				}
				timeout (time:3, unit:'MINUTES') {
					sh 'echo "Time check for health"'
				}
			}
		}
		stage('Test') {
			steps {
				sh 'echo "Passed";exit 0'
			}
		}
	}
	post {
		always {
			echo 'This will always run'
		}
		success {
			echo 'This will run only when successful'
		}
		failure {
			echo 'This will run only on failure'
		}
	}
}
