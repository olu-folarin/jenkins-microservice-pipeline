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
		// to locate their home folders and get their paths
		// dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$mavenHome/bin:$PATH"
	}
	
	stages {
		stage('Checkout') {
			steps {
				// after finding the paths, you can now get both docker and maven versions
				sh 'mvn --version'
				// sh 'docker version'
				echo "Build"
				// using some global variables
				echo "$PATH"
				echo "TAG_NAME- $env.TAG_NAME"
				echo "TAG_DATE - $env.TAG_DATE"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "BUILD_NAME - $env.BUILD_NAME"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "JOB_ID - $env.JOB_ID"
			}
		}
		stage('Compile') {
			steps {
				// compile the code
				sh 'mvn clean compile'
			}
		}
		stage('Test') {
			steps {
				sh 'mvn test'
			}
		}
		stage('Integration Test') {
			steps {
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}
		stage('Build Docker Image') {
			steps {
				// enter the image name
				// docker build -t in28min/currency-exchange-devops:$env.BUILD_TAG

				// an easier way to do this is with a script
				script {
					docker.build("in28min/currency-exchange-devops:${$env.BUILD_TAG}")
				}
			}
		}
		stage('Push Docker Image') {
			steps {
				// push to dockerhub
				steps {
					script {
						dockerImage.push();
						// push the latest version/integration
						dockerImage.push('latest')
					}
				}
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