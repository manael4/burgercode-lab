pipeline {
    agent any

    stages {
        stage('Checkout (Ingredientes)') {
            steps {
                echo 'Descargando la receta de BurgerCode...'
                // Descarga el código desde el repositorio configurado en Jenkins
                checkout scm [cite: 95, 96]
            }
        }

        stage('Build (Cocinar)') {
            steps {
                echo 'Cocinando la imagen Docker...'
                // Crea la imagen de Docker usando el Dockerfile del repo
                sh 'docker build -t burgercode-app .' [cite: 101, 102]
            }
        }

        stage('Test (Control de Calidad)') {
            steps {
                echo 'Probando la hamburguesa...'
                // Ejecuta el test.py dentro del contenedor recién creado
                sh 'docker run --rm burgercode-app python test.py' [cite: 107, 110]
            }
        }

        stage('Deploy (Entrega)') {
            steps {
                echo 'Desplegando en Producción...'
                // Elimina el contenedor anterior si existe para evitar conflictos
                sh 'docker rm -f burger-prod || true' [cite: 116, 117]
                // Lanza la nueva versión en el puerto 5000
                sh 'docker run -d --name burger-prod -p 5000:5000 burgercode-app' [cite: 118]
                echo '¡Hamburguesa servida en http://localhost:5000!' [cite: 119]
            }
        }
    }
}
