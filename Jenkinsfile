pipeline {
    agent any
     stages {
        stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                '''
            }
          }
        stage ('Build') {
            steps 
                {
                dir('/src/pom.xml'){
                sh 'mvn clean package'
            }
        }
      }

        stage ('Deploy to Octopus') {
            steps {
                withCredentials([string(credentialsId: 'OctopusAPIKey', variable: 'APIKey')]) {
                    sh """
                        ${tool('Octo CLI')}/Octo push --package target/gs-maven-0.1.0.jar --replace-existing --server https://https://satya.octopus.app --apiKey ${APIKey}
                        ${tool('Octo CLI')}/Octo create-release --project "deploy_test-1" --server https://https://satya.octopus.app --apiKey ${APIKey}
                        ${tool('Octo CLI')}/Octo deploy-release --project "deploy_test-1" --version latest --deployto Integration --server https://https://satya.octopus.app --apiKey ${APIKey}
                    """
                }
            }
        }
    }
}
