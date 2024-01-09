pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    // Define Docker build command
                    def dockerImage = docker.build('jenkins_test_two')

                    // Tag the built image
                    dockerImage.tag "nadgesachin/jenkins_test_two:${env.BUILD_NUMBER}"
                }
            }
        }
        // Add more stages as needed for testing, deployment, etc.
    }

    post {
        success {
            // Push the Docker image to a registry
            script {
                docker.withRegistry('https://index.docker.io/v1/', 'docker_hub') {
                    def dockerImage = docker.image("nadgesachin/jenkins_test_two:${env.BUILD_NUMBER}")
                    dockerImage.push()
                }
            }
        }
    }
}
