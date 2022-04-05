pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('docker-cred-sohail')
	}

	stages {

		stage('Build') {

			steps {
				sh 'docker build -t sohailquazi/springboot-app:latest .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push sohailquazi/springboot-app:latest'
			}
		}
	}

	// post {
	// 	always {
	// 		sh 'docker logout'
	// 	}
	// }

}
