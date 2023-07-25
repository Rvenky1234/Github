pipeline {
agent any
stages {
// Checkout the code in Stage SCM
stage('scm') {
steps {
echo "Pulling changes from branch feature-dev/quantum-22.1.0 and from repo K1_SERVICE"
checkout poll: false, scm: [$class: 'GitSCM', branches: [[name: "master"]],
doGenerateSubmoduleConfigurations: false,
                           extensions: [[$class: 'CleanBeforeCheckout']],
extensions: [[$class: 'CloneOption', depth: 1, noTags: false, reference: '', shallow: true]],
gitTool: 'Default', submoduleCfg: [],
                           userRemoteConfigs: [[credentialsId: '',
url: "https://github.com/Rvenky1234/javaparser-maven-sample.git"]]
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
jdk 'java'
maven 'maven'
  }
steps {
echo "Starting Build"
sh 'mvn clean install'
echo 'Clean Install Completed'        
}
}
stage('Docker stage') {
steps {
echo "Building image"
sh 'docker build -t images .'   
}
}
stage('Docker push') {
      steps {
        sh'''
          docker login  --username rvenkat1234 --password Venky@007
          docker tag images:latest rvenkat1234/cloudbackup1234:${version_NUMBER}
          docker push rvenkat1234/cloudbackup1234:${version_NUMBER}
        '''
      }
}
}
}
