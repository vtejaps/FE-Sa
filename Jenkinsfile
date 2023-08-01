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

        stage('Sonar Analysis') {
            steps {
                script {
                    withSonarQubeEnv(credentialsId: 'Sonar') {
                        sh "echo '${env.SUDO_PASSWORD}' | sudo -S /opt/Sonar-scanner/bin/sonar-scanner -Dsonar.projectName=FE-Sample -Dsonar.projectKey=FE-Sample"
                    }
                }
            }
        }
    }
}
