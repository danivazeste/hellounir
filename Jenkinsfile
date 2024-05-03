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

        stage('UnitRest') {
            steps {
                catchError(buildResult: 'UNSTABLE', stageResult: 'FAILURE') {
                    bat '''
                        set FLASK_APP=app\\api.py
                        start flask run
                        
                        set PYTHONPATH=%WORKSPACE%
                        pytest --junitxml=result-unit.xml test/rest
                    '''
                }
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
