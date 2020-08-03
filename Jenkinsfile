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
				echo "mvn clean compile"
			}
		}
		stage('Test'){
			steps {
				echo " mvn test"
			}
		}
		stage('Integration Test'){
			steps {
				echo " mvn failsafe:integration-test failsafe:verify"
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
