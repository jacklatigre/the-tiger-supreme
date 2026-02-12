pipeline {
    agent any
    environment {
        DOCKER_USER = 'il_tuo_utente_dockerhub' 
        IMAGE_NAME  = 'the-tiger-app'
    }
    stages {
        stage('Build & Push') {
            steps {
                script {
                    sh "docker build -t ${DOCKER_USER}/${IMAGE_NAME}:latest ./app"
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-creds', passwordVariable: 'DOCKER_PASS', usernameVariable: 'DOCKER_USER_VAR')]) {
                        sh "echo $DOCKER_PASS | docker login -u $DOCKER_USER_VAR --password-stdin"
                        sh "docker push ${DOCKER_USER}/${IMAGE_NAME}:latest"
                    }
                }
            }
        }
    }
}
