node(label: 'builder') {
  agent {label 'builder'}
  def myGradleContainer = docker.image('gradle:jdk8-alpine')
  myGradleContainer.pull()
  stage('prep') {
    checkout scm
  }
  stage('test') {
     myGradleContainer.inside("-v ${env.HOME}/.gradle:/home/gradle/.gradle") {
       sh 'cd complete && gradle -g gradle-user-home test'
     }
  }
  stage('run') {
     myGradleContainer.inside("-v ${env.HOME}/.gradle:/home/gradle/.gradle") {
       sh 'cd complete && gradle -g gradle-user-home run'
     }
  }
}
