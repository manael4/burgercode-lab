pipeline {
    agent any

    stages {
        stage('Checkout (Ingredientes)') {
            steps {
                echo 'Descargando la receta de BurgerCode...'
                checkout scm
            }
        }

        stage('Build (Cocinar)') {
            steps {
                echo 'Cocinando la imagen Docker...'
                sh 'docker build -t burgercode-app .'
            }
        }

        stage('Test (Control de Calidad)') {
            steps {
                echo 'Probando la hamburguesa...'
                // Ejecutamos el test dentro del contenedor recién creado [cite: 108, 110]
                sh 'docker run --rm burgercode-app python test.py'
            }
        }

        stage('Deploy (Entrega)') {
            steps {
                echo 'Desplegando en Producción...'
                // Limpiamos el contenedor anterior si existe [cite: 117]
                sh 'docker rm -f burger-prod || true'
                // Desplegamos la nueva versión en el puerto 5000 [cite: 118]
                sh 'docker run -d --name burger-prod -p 5000:5000 burgercode-app'
                echo '¡Hamburguesa servida en http://localhost:5000!'
            }
        }
    }

    // El bloque post gestiona la limpieza y notificaciones finales [cite: 175]
    post {
        always {
            echo 'Limpiando la cocina...'
            // Borra imágenes intermedias para ahorrar espacio [cite: 178]
            sh 'docker image prune -f'
        }
        success {
            echo '🎉 ¡Pipeline completado con éxito!'
        }
        failure {
            echo '🚑 ¡ALERTA! El pipeline ha fallado. Revisar logs.'
        }
    }
}
