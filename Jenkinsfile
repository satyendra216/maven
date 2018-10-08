node {
  stage('SCM checkout'){
checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'GITCRED', url: 'https://github.com/satyendra216/maven.git']]])
}
  stage('compile-package'){
	sh 'mvn package'
}
}
