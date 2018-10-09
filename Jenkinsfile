node {
     tools {
        jdk 'java 10'
}
  stage('SCM checkout'){
checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'GITCRED', url: 'https://github.com/satyendra216/maven.git']]])
}

  stage('compile-package')
       {
        def mvnHome = tool name: 'Maven', type: 'maven'
	sh "${mvnHome}/bin/mvn package"
}
}
