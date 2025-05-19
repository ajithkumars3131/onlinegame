pipeline {
    agent any
    tools{
        jdk 'jdk17'
        nodejs 'node16'
    }
   
    stages {
        stage('Clean') {
            steps {
                  cleanWs()
            }
        }
        stage('sonarqube-check'){
            steps{
             
               withSonarQubeEnv('sonarqube')  {
                   sh ''' 	
                       /opt/sonar-scanner/bin/sonar-scanner \
                           -Dsonar.projectKey=akworld-onelinegame \
                            -Dsonar.sources=. \
                            -Dsonar.host.url=http://34.72.160.36:9000 \
                            -Dsonar.token=sqp_ac3daf90c479db3418bca1a876d2e7efbab1b023 '''
    
                 } 

              
            }
        }
    }
}
