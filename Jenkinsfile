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
	stages{
		stage('Build and test'){
			steps{
				// sh 'mvn --version'
				// sh 'node --version'
				echo "Build"
				echo "Test"
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