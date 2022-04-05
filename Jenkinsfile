pipeline {
    agent any
    // tools {
    //     maven 'maven-3.6.3' 
    // }
    environment {
        DATE = new Date().format('yy.M')
        TAG = "${DATE}.${BUILD_NUMBER}"
    }
    stages {
        stage ('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage ("Build Docker Image") {

            steps{

                     sh 'docker build -t sohailquazi/springboot-app:${TAG} .'

                }

            }
        // stage('Docker Build') {
        //     steps {
        //         // script {
        //         //     docker.build("sohailquazi/springboot-app:${TAG}")
        //              sh 'docker run -p 8090:8090 sohailquazi/springboot-app:${TAG}'
        //         }
        //     }
        
	    stage ('Pushing Docker Image to Dockerhub') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker_credential') {
                        docker.image("sohailquazi/springboot-app:${TAG}").push()
                        docker.image("sohailquazi/springboot-app:${TAG}").push("latest")
                    }
                    //  sh 'docker push sohailquazi/springboot-app:${TAG}'
                }
            }
        }
        
        stage('Deploy'){
            steps {
                sh "docker stop hello-world | true"
                sh "docker rm hello-world | true"
                sh "docker run --name hello-world -d -p 8090:8090 sohailquazi/springboot-app:${TAG}"
            }
        }
    }
}
