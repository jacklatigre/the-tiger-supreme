pipeline {
    agent any
    
    environment {
        // CAMBIA 'il_tuo_username_qui' con il tuo nome utente Docker Hub (es. jacklatigre)
        DOCKER_USER = 'giacomo12305' 
        IMAGE_NAME  = 'the-tiger-app'
    }

    stages {
        stage('Build & Push') {
            steps {
                script {
                    // 1. Build dell'immagine Docker usando il Dockerfile nella cartella /app
                    sh "docker build -t ${DOCKER_USER}/${IMAGE_NAME}:latest ./app"
                    
                    // 2. Login e Push su Docker Hub usando le credenziali salvate in Jenkins
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-creds', passwordVariable: 'DOCKER_PASS', usernameVariable: 'DOCKER_USER_VAR')]) {
                        sh "echo \$DOCKER_PASS | docker login -u \$DOCKER_USER_VAR --password-stdin"
                        sh "docker push ${DOCKER_USER}/${IMAGE_NAME}:latest"
                    }
                }
            }
        }
    }
}
