pipeline {

    
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('dihiabelarbia')
    }
    stages { 

        
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t myapp/flask:$BUILD_NUMBER .'
            }
        } 
        
        stage('push image') {
            steps{
                sh 'docker push myapp/flask:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}
