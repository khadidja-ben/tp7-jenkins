pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat 'D:\\SCHOOL\\SIL2\\S1\\done\\Outils\\TPs\\Gradle\\gradle-5.6\\bin\\gradle build'
        bat 'D:\\SCHOOL\\SIL2\\S1\\done\\Outils\\TPs\\Gradle\\gradle-5.6\\bin\\gradle javadoc'
        archiveArtifacts 'build/docs/javadoc/*'
        archiveArtifacts 'build/reports/tests'
      }
      post {
        always {
          echo " Build stage complete "
        }
        failure {
          echo "Build failed"
        }
        success {
          echo "Build succeeded"
        }
      }
    stage('Mail Notification') {
      steps {
        mail(cc: 'hk_bennamane@esi.dz', subject: 'build', body: 'new build')
      }
    }

  }
}
