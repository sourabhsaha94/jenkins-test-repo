pipeline {
	agent any
	stages {
		stage('Build') {
			steps {
				sh 'javac src/TestMain.java'
            		}
        	}
		stage('Deploy'){
			steps {
				retry(3) {
					sh 'echo "This is deploy stage"'
					sh '''
					cd src/ 
					java TestMain
					echo 'Main-Class: TestMain' > manifest.txt
					jar cvfm SampleJar.jar manifest.txt *.class
					cd ..
					mkdir test
					cp src/SampleJar.jar test/
					cd test/
					java -jar SampleJar.jar > ../output.txt
					cd ..'''
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
