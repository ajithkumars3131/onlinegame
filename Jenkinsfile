pipeline {
    agent any
    tools{
        jdk 'jdk17'
        nodejs 'node16'
    }
    environment {
        SCANNER_HOME=tool 'SonarQube'
    }
    stages {
        stage('Clean') {
            steps {
                  cleanWs()
            }
        }
        stage('Checkout-new') {
           steps {
             git branch: 'main', url: 'https://github.com/ajithkumars3131/onlinegame.git'
            }
        }
         stage('SonarQube Analysis') {
            steps {
               withSonarQubeEnv('SonarQube-Server') {
                   sh '''    
                        /var/lib/jenkins/tools/hudson.plugins.sonar.SonarRunnerInstallation/SonarQube/bin/sonar-scanner \
                        -Dsonar.projectKey=akworld-online \
                        -Dsonar.sources=. \
                        -Dsonar.host.url=http://35.200.197.171:9000 \
                        -Dsonar.token=sqa_494fb06170008af241569900c3790d4e012a3a84
                      '''
                     
                }
            } 
        }
         stage('Quality Gate Check') {
           steps{
               script {
                 waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token'
                      }    
                }
        } 
        stage('Install Dependencies') {
            steps{
                sh "npm install"
            }
        }
        stage('OWASP FS SCANs') {
             steps {
                dependencyCheck additionalArguments: '--scan ./ --disableYarnAudit --disableNodeAudit', odcInstallation: 'DP'
                dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }

        }
        post {
        always {
            archiveArtifacts artifacts: '**/dependency-check-report.*', allowEmptyArchive: true
            cleanWs() 
    
        }
    
    }





}
}
