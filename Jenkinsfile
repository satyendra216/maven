pipeline {
    agent any

        stage ('Build') {
            steps {
                sh 'mvn package'
            }
        }

        stage ('Deploy to Octopus') {
            steps {
                withCredentials([string(credentialsId: 'OctopusAPIKey', variable: 'APIKey')]) {
                    sh """
                        ${tool('Octo CLI')}/Octo push --package target/deploy_test-1-SNAPSHOT.war --replace-existing --server https://youroctopusserver --apiKey ${APIKey}
                        ${tool('Octo CLI')}/Octo create-release --project "deploy_test-1" --server https://youroctopusserver --apiKey ${APIKey}
                        ${tool('Octo CLI')}/Octo deploy-release --project "deploy_test-1" --version latest --deployto Integration --server https://youroctopusserver --apiKey ${APIKey}
                    """
                }
            }
        }
    }

