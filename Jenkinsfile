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
             git clone 'https://github.com/ajithkumars3131/onlinegame.git', branch: 'main'
            }
        }  
    }    
}

#