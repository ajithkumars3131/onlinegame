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
        stage('Checkout-new') {
           steps {
             git branch: 'main', url: 'https://github.com/ajithkumars3131/onlinegame.git'
            }
        }  
    }    
}

#