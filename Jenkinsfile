pipeline {

     agent any

    tools {nodejs 'node 20'}

    environment {

        CHROME_BIN = '/bin/google-chrome'

    }

    stages {
        stage('Dependencies') {
            steps {
bat 'npm cache clean --force'
bat 'npm install'
bat 'npm i @badeball/cypress-cucumber-preprocessor@latest'
bat 'npm install cypress --save-dev'

                
                                
            }
        }


         stage('Test Execution') {

            steps {

                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE'){
                bat 'npm run cypress:regression:test'}

            }

         }
     
      stage('Generate HTML Report') {
            steps {
                bat 'npm run generate:report'
                 cucumber buildStatus: 'UNSTABLE',
                    reportTitle: 'My report',
                    fileIncludePattern: 'reports/cucumber-htmlreport.html/jsonlogs/log.json',
                    trendsLimit: 10,
                    classifications: [
                        [
                            'key': 'Browser',
                            'value': 'chrome'
                        ]
                    ]
            }
         }  

 
        stage('Imprimo log txt'){
            steps {
                bat 'npm run generate:report:txt'
                 script {
                    def data = readFile(file:'reportsTXT/Reporte.txt')
                    println(data)
                } 

            }

 

        }


    }


}
