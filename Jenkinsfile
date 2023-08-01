pipeline {
    agent {
        node {
            label "ubuntu-PS"
        }
    }

   /* tools {
        sonarqubeScanner "Sonar"
    } */

    stages {
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }

        /* stage('Credentials') {
            steps {
                script {
                    def sudoPassword = input(
                        id: 'sudo-password',
                        message: 'Enter sudo password:',
                        parameters: [
                            [$class: 'PasswordParameterDefinition', description: 'Sudo password', name: 'SUDO_PASSWORD']
                        ]
                    ).toString()
                    sh 'echo "$sudoPassword"'
                }
            }
        } */

        stage('Sonar') {
            steps {
                script {
                    withSonarQubeEnv(credentials: 'sonar') {
                        sh /* "echo '${SUDO_PASSWORD}' | */ 'sudo -S /opt/Sonar-scanner/bin/sonar-scanner -Dsonar.projectName=test2 -Dsonar.projectKey=test2'
                    }
                }
            }
        }
    }
}
