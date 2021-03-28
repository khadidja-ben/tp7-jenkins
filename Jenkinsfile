pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat 'D:\\SCHOOL\\SIL2\\S1\\done\\Outils\\TPs\\Gradle\\gradle-5.6\\bin\\gradle build'
        bat 'D:\\SCHOOL\\SIL2\\S1\\done\\Outils\\TPs\\Gradle\\gradle-5.6\\bin\\gradle javadoc'
        archiveArtifacts 'build/libs/*.jar'
        archiveArtifacts 'build/docs'
        archiveArtifacts 'build/reports/tests'
      }
    }

  }
}