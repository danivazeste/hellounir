pipeline {
    agent any
    stages {
        stage('Get Code') {
            steps {
                // Obtener código del repositorio
                git 'https://github.com/danivazeste/hellounir.git'
            }
        }

        stage('Unit') {
            steps {
                //Test UNIT
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
        	//Test REST con lanzamiento de microservicios
                catchError(buildResult: 'UNSTABLE', stageResult: 'FAILURE') {
                     bat '''
                            set FLASK_APP=app\\api.py
                            start flask run
                            start java -jar C:\\Users\\yog19\\Desktop\\CP1UNIR\\software\\wiremock-standalone-3.5.4.jar --port 9090 --root-dir test\\wiremock
                            exit
                            set PYTHONPATH=%WORKSPACE%
                            pytest --junitxml=result-rest.xml test/rest
                            '''
                        }
                    }
                }


        stage('Static') {
            steps {
		catchError(buildResult: 'SUCCESS', stageResult: 'UNSTABLE'){
                bat '''
                    flake8 --exit-zero --format=pylint app >flake8.out
		    '''
		recordIssues tools: [flake8(name: 'Flake8', pattern: 'flake8.out')], qualityGates : [[threshold: 8, type: 'TOTAL', unstable: true], [threshold: 10, type: 'TOTAL', unstable: false]]}
            }
        }
    
    }
}
