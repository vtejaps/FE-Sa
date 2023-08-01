pipeline {
    agent {
        node {
            label "ubuntu-PS"
        }
    }

     tools {
        sonarqubeScanner "Sonar"
    } 

    stages {
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                 // script {
                    def scannerHome = tool 'Sonar';
                    withSonarQubeEnv('Sonar') {
                    //    sh "${scannerHome}/bin/sonar-scanner"
                   // } 
                }
            }
        }  
    }
}
