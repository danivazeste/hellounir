pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                // HELLO WORLD
                echo 'Hello World'
            }
        }

        stage('Get Code') {
            steps {
                // Obtener código del repositorio
                git 'https://github.com/danivazeste/hellounir.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Esto es Python. No hay que compilar nada!!!'
                echo WORKSPACE
                bat 'dir'
            }
        }

        stage('Unit') {
            steps {
                bat '''
                    set PYTHONPATH=.
                    pytest test\\unit
                    pytest --junitxml=result-unit.xml test/unit
                '''
            }
        }

        stage('Results') {
            steps {
                // Ficheros de resultado
                junit 'result*.xml'
                echo 'FINISH!!!'
            }
        }
    }
}
