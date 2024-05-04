pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                // HELLO WORLD
                echo 'Hello World desde Caso Práctico 1 de Daniel Vázquez Esteban'
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
                //Build que muestra el WORKSPACE y directorio de trabajo.
                echo 'Esto es Python. No hay que compilar nada!!!'
                echo WORKSPACE
                bat 'dir'
            }
        }

        stage('Tests') {
            parallel {

                stage('Unit') {
                    steps {
                        catchError(buildResult: 'UNSTABLE', stageResult: 'FAILURE') {
                            bat '''
                                set PYTHONPATH=%WORKSPACE%
                                pytest --junitxml=result-unit.xml test/unit
                            '''
                        }
                    }
                }
        
                stage('Rest') {
                    steps {
                        catchError(buildResult: 'UNSTABLE', stageResult: 'FAILURE') {
                            bat '''
                                set FLASK_APP=app\\api.py
                                start flask run
                                start java -jar C:\\Users\\yog19\\Desktop\\CP1UNIR\\software\\wiremock-standalone-3.5.4.jar --port 9090 --root-dir test\\wiremock
                                waitfor SomethingThatIsNeverHappening /t 10 >nul
                                set PYTHONPATH=%WORKSPACE%
                                pytest --junitxml=result-rest.xml test/rest
                            '''
                        }
                    }
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
