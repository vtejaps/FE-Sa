pipeline {
    agent {
        node {
            label "ubuntu-PS"
        }
    }

    /* tools {
        nodejs "Nodejs"
    } */

    stages {
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('SonarQube Analysis') {
            def scannerHome = tool 'SonarScanner';
            withSonarQubeEnv() {
                sh "${scannerHome}/bin/sonar-scanner"
            }
        }
    }
}
