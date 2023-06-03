pipeline {
    agent any

    stages {
        stage('Clonar repositorio') {
            steps {
                git branch: 'quality',
                    credentialsId: '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',
                    url: 'https://github.com/richifor/ventabus.git'
            }
        }

        stage('Preparación') {
            steps {
                sh 'echo "usuario que ejecuta las tareas $USER"'
                //sh 'apt-get update'
                //sh 'apt-get install -y python3-pip'
                sh 'pip3 install flask flask_restful flask_sqlalchemy pylint'
            }
        }

        stage('Verificación de calidad de código') {
            steps {
               sh 'echo "control de calidad de código. Testear el porcentaje con pylint"'
                //sh 'pylint bus/srv_bus.py registro/registro.py cajero/caja.py tienda/tienda.py'
               //sh 'pylint bus/srv_bus.py registro/registro.py cajero/caja.py tienda/tienda.py'
            }
        }

        stage('Construcción de imágenes Docker') {
            steps {
                sh 'docker compose build'
            }
        }

        stage('Pruebas unitarias') {
            steps {
                sh 'python3 -m unittest testunitarios.test_srv_bus'
                sh 'python3 -m unittest testunitarios.test_registro'
            }
        }

        stage('Despliegue') {
            steps {
                sh 'docker compose up -d'
            }
        }
    }
}
