pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                // Clonar el repositorio
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Construir la imagen Docker
                    docker.build('fastapi-app:latest')
                }
            }
        }

        stage('Run Docker Image') {
            steps {
                script {
                    // Ejecutar el contenedor para probar
                    sh '''
                    docker run -d -p 8000:8000 --name fastapi-test fastapi-app:latest
                    sleep 5
                    curl -f http://localhost:8000 || exit 1
                    docker stop fastapi-test
                    docker rm fastapi-test
                    '''
                }
            }
        }
    }
}
