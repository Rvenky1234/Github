pipeline {
agent any
stages {
// Checkout the code in Stage SCM
stage('scm') {
steps {
echo "Pulling changes from branch feature-dev/quantum-22.1.0 and from repo K1_SERVICE"
checkout poll: false, scm: [$class: 'GitSCM', branches: [[name: "main"]],
doGenerateSubmoduleConfigurations: false,
                           extensions: [[$class: 'CleanBeforeCheckout']],
extensions: [[$class: 'CloneOption', depth: 1, noTags: false, reference: '', shallow: true]],
gitTool: 'Default', submoduleCfg: [],
                           userRemoteConfigs: [[credentialsId: '',
url: "https://github.com/Rvenky1234/Github.git"]]
  ]
}
}
stage ('JDK_11') {
   tools {
jdk 'java'
}
   steps{
     sh '''
java -version
'''
          }
  }

// Reading build properties into buildProps

stage('Maven BUILD') {
tools {
jdk "java"
  }
steps {
echo "Starting Build"
sh 'mvn clean install'
echo 'Clean Install Completed'        
}
}
}
}
