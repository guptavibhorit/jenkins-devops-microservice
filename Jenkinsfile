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
		stage('Build'){
			steps {
				//sh 'mvn --version'
				//sh 'node -version'
				echo "Build"
				echo "PATH - $PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_URL"
				
			}
		}
		stage('Test'){
			steps {
				echo "Test"
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
