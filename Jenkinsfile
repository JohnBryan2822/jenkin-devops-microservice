// SCRIPTED

// node {
// 	stage('Build') {
// 		echo "Build"
// 	}
// 	stage('Test') {
// 		echo "Test"
// 	}
// 	stage('Test') {
// 		echo "Test"
// 	}
// }

// DECLARATIVE
pipeline {
	// agent { docker {image 'maven:3.6.3'} }
	// agent { docker {image 'node:13.8'} }
	agent any
	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages{
		stage('Build and test'){
			steps{
				sh 'mvn --version'
				sh 'docker version'
				echo "Build"
				echo "Test"
				echo "PATH - $PATH"
				echo "Build_number - $env.BUILD_NUMBER"
				echo "Build_ID - $env.BUILD_ID"
				echo "JOB-NAME - $env.JOB_NAME"
				echo "Build_tag - $env.BUILD_TAG"
				echo "Build_URL - $env.BUILD_URL"
			}
		}
		stage('Integration test'){
			steps{
				echo "Integration test"
			}
		}
	}
	post {
		always {
			echo 'I run always'
		}
		success {
			echo 'I run when you are successful'
		}
		failure {
			echo 'I run when you are fail'
		}
	}
}