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

	// configuring docker and maven with environment
	environment {
		// to locate their home folders
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'

		// 
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages {
		stage('Build') {
			steps {
				// after finding the paths, you can now get both docker and maven versions
				sh 'mvn --version'
				sh 'docker --version'
				echo "Build"
				// using some global variables
				echo "$PATH"
				echo "TAG_NAME- $env.TAG_NAME"
				echo "TAG_DATE - $env.TAG_DATE"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "BUILD_NAME - $env.BUILD_NAME"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "JOB_ID - $env.JOB_ID"
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
			echo 'The build was successful.'
		}
	}
}