pipeline {
    agent any

    stages {
        stage('Limpieza Inicial') {
            steps {
                // Detiene contenedores previos para evitar conflictos de puertos (5000:5000)
                sh 'docker-compose down --remove-orphans'
            }
        }

        stage('Build & Test') {
            steps {
                // Construye la imagen basada en tu carpeta ./app y tu dockerfile
                sh 'docker-compose build'
            }
        }

        stage('Deploy Local') {
            steps {
                // Levanta el servicio en segundo plano
                sh 'docker-compose up -d'
                echo 'Aplicación desplegada en http://localhost:5000'
            }
        }
    }
    
    post {
        failure {
            echo 'Algo salió mal en el pipeline. Revisa los logs de Docker.'
        }
    }
}