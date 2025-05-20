pipeline {
    agent any
    tools {
        jdk 'jdk17'
        nodejs 'node16-new'
    }
    environment {
        SCANNER_HOME = tool 'SonarQube'
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
                        -Dsonar.token=sqp_646aab6bf3861d6f3912fc4a10212da318813e44
                    '''
                }
            } 
        }
        stage('Quality Gate Check') {
            steps {
                script {
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token'
                }    
            }
        } 
        stage('Install Dependencies') {
            steps {
                sh "npm install"
            }
        }
        stage('OWASP FS SCANs') {
            steps {
                dependencyCheck additionalArguments: '--scan ./ --disableYarnAudit --disableNodeAudit', odcInstallation: 'DP'
                dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }
    
     stage('Trivy FS Scanning') {
            steps {
                sh "trivy fs . > trivyscanreport.txt"
            }
        }
     stage('Docker Build using the Dockerfile and then push it to DockerHub') {
            steps {
               script {
                   withDockerRegistry(credentialsId: 'docker', toolName: 'docker') {
                   sh "docker build -t onlinegame . "
                   sh "docker tag onlinegame ajithkumars3131/onlinegamet:latest"
                   sh "docker push ajithkumars3131/onlinegame:latest "
                 }
               }
            }
        }
        
    }
}
