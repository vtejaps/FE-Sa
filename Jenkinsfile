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

        stage('Credentials') {
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
                    // Save the password to an environment variable for later use
                    env.SUDO_PASSWORD = sudoPassword
                }
            }
        }

        stage('Sonar') {
            steps {
                script {
                    def scannerHome = tool 'Sonar'
                    withSonarQubeEnv(credentialsId: 'Sonar-token') {
                        sh "echo '${env.SUDO_PASSWORD}' | sudo -S ${scannerHome}/bin/sonar-scanner -Dsonar.projectName=FE-Sample -Dsonar.projectKey=FE-Sample"
                    }
                }
            }
        }
    }
}
