pipeline {
    agent any 

    environment {
        // Define DockerHub credentials using Jenkins credentials
        DOCKERHUB_CREDENTIALS = credentials('dihiabelarbia')
    }

    stages { 
        stage('Build Docker Image') {
            steps {  
                // Build Docker image with a tag including the build number
                sh 'docker build -t dihiabelarbia/flask:${BUILD_NUMBER} .'
            }
        } 

        stage('Login to DockerHub') {
            steps{
                    // Use the credentials to login to DockerHub
                    sh 'echo "${DOCKERHUB_CREDENTIALS_PSW}" | docker login -u "${DOCKERHUB_CREDENTIALS_USR}" --password-stdin'
                }
        }
        
        stage('Push Image') {
            steps {
                // Push the Docker image to DockerHub
                sh 'docker push dihiabelarbia/flask:${BUILD_NUMBER}'
            }
        }
    }

    post {
        always {
            // Logout from DockerHub after the build is complete
            sh 'docker logout'
        }
    }


    
}
