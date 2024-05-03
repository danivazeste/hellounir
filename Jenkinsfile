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

        stage('Unit') {
            steps {
                bat '''
                    set PYTHONPATH='C:\Users\yog19\AppData\Roaming\Python\Python311\Scripts\'
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
