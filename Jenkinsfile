pipeline {
agent {
  label 'master'
}

triggers {
  pollSCM ''
}
options {
        skipDefaultCheckout(true)
        // Keep the 10 most recent builds
        buildDiscarder(logRotator(numToKeepStr: '10'))
        timestamps()
}

environment {
  VERSION = "jelly"
}
stages{
stage('details') {
  steps {
         echo "Running ${env.BUILD_ID} on {env.JENKINS_URL}"
         echo "${env.VERSION}"
  }

  when {
    environment name: 'VERSION', value: 'jelly'
  }
}


stage('checkout') {
  steps {
      checkout([$class: 'GitSCM', 
      branches: [[name: '*/main']],
      doGenerateSubmoduleConfigurations: false,
      extensions: [],
      submoduleCfg: [],
      userRemoteConfigs: [[credentialsId: '8f5cfa58-af1a-4df4-878a-db8bfaab4133',
      url: 'https://github.com/Joseph-igbi/simple-app.git']]])
  }
}


stage('build') {
  steps {
     sh 'pip3 install -r requirements.txt'
  }
}

stage('test') {
  steps {
      sh 'python3 test.py'
     
  }
}
    


}




}
