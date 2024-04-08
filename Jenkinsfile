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
		stage('Checkout'){
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

		stage ('Compile') {
			steps {
				sh "mvn clean compile"
			}
		}

		stage('Integration test'){
			steps{
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}

		stage('Package') {
			steps {
				sh "mvn package -DskipTests"
			}
		}

		stage('Build Docker Image'){
			steps {
				// docker build -t johnbryan2822/currency-exchange-with-jenkins:$env.BUILD_TAG
				script {
					dockerImage = docker.build("johnbryan2822/currency-exchange-with-jenkins:${env.BUILD_TAG}")
				}
			}
		}

		stage('Push Docker Image') {
			steps {
				script {
					docker.withRegistry('', 'dockerhub') {
						dockerImage.push();
						dockerImage.push('latest');
					}
				}
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