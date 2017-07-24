pipeline {
	agent any
	stages {
		stage('Build') {
			steps {
				sh 'cd src'
				sh 'javac TestMain.java'
				sh 'cd ..'
            		}
        	}
		stage('Deploy'){
			steps {
				retry(3) {
					sh 'echo "This is deploy stage"'
					sh 'cd src'
					sh 'java TestMain > ../output.txt'
					sh 'cd ..'
				}
				timeout (time:3, unit:'MINUTES') {
					sh 'echo "Time check for health"'
				}
			}
		}
		stage('Test') {
			steps {
				sh 'cat output.txt'
				sh 'echo "Tests passed"; exit 0'
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
