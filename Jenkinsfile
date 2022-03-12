// scripted pipeline
// node {
// 	stage('Build') {
// 		echo "Build"
// 	}
// 	stage('Test') {
// 		echo "Test"
// 	}
// 	stage ('Integration Test') {
// 		echo "Integration Test"
// 	}
// }


// Declarative syntax/pipeline: modern
pipeline {
	// (the agent refers to where ur build will run)
	agent any
	stages {
		stage('Build') {
			steps {
				echo "Build"
			}
		}
		stage('Test') {
			steps {
				echo "Test"
			}
		}
		stage('Integration Test') {
			steps {
				echo "Integration Test"
			}
		}
	} 
	
	post {
		always {
			echo 'I run all the time!'
		}
		success {
			echo 'I only run when you are successful! Yippeee :)'
		}
		failure {
			echo 'I stall whenever your pipeline fails!'
		}
		changed {
			echo 'The build was successful'
		}
		changed {
			echo 'The build failed'
		}
	}
}