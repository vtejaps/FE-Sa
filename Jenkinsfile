pipeline {
    agent {
        node {
            label "ubuntu-PS"
        }
    }

    tools {
        nodejs "Nodejs"
    }

    stages {
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }
    }
}
