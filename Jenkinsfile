pipeline {
    agent any

    stages {
        stage('Clean') {
            steps {
                  cleanWs()
            }
        }
        stage('sonarqube-check'){
            steps{
              withEnv(["PATH=${env.PATH}:/opt/sonar-scanner/bin"]) {
                   sh ''' 	
                       sonar-scanner \
                          -Dsonar.projectKey=Bingoonelinegame \
                          -Dsonar.sources=. \
                          -Dsonar.host.url=http://34.46.17.202:9000 \
                          -Dsonar.login=sqa_f850199be1f7543719fbd609586d1ae6d86a7952 '''
    
                } 


            }
        }
    }
}
