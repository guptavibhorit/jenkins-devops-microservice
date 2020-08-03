//DECLARATIVE
pipeline {
	agent any
	//agent {docker {image 'maven:3.6.3'} }
	//agent {docker {image 'node:13.8'} }
	environment{
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages{
		stage('Checkout'){
			steps {
				sh 'mvn --version'
				//sh 'node -version'
				sh 'docker version'
				echo "Build"
				echo "PATH - $PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_URL"
				
			}
		}
		stage('Compile'){
			steps {
				sh "mvn clean compile"
			}
		}
		stage('Test'){
			steps {
				sh "mvn test"
			}
		}
		stage('Integration Test'){
			steps {
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}
		stage('Package'){
			steps {
				sh "mvn package -DskipTests"
			}
		}
		stage('Build Docker Image'){
			steps {
				//"docker build -t guptavibhorit/currency-exchange-devops:$env.BUILD_TAG"
				script{
					dockerImage = docker.build("guptavibhorit/currency-exchange-devops:${env.BUILD_TAG}")
				}
			}
		}
		stage('Push Docker Image'){
			steps {
				script{
					docker.withRegistry('', 'dockerhub') {
						dockerImage.push();
						dockerImage.push('latest');
					}
				}
			}
		}
    } 

	post{

		always{
			echo "I will always run"
		}
		success{
			echo "I will only run when build is successful"
		}

		failure{
			echo "I will only run when build fails"
		}

	}
	
}

//SCRIPTED
//node {
//    stage('Build') {
//        echo "Build"
//    }
//   stage('Test') {
//        echo "Test"
//    }
//}
