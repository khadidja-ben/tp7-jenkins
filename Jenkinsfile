pipeline {
  agent any
  stages {
    stage('Build') {
      post {
        always {
          echo ' Build stage complete '
        }

        failure {
          echo 'Build failed'
        }

        success {
          echo 'Build succeeded'
        }

      }
      steps {
        bat 'D:\\SCHOOL\\SIL2\\S1\\done\\Outils\\TPs\\Gradle\\gradle-5.6\\bin\\gradle build'
        bat 'D:\\SCHOOL\\SIL2\\S1\\done\\Outils\\TPs\\Gradle\\gradle-5.6\\bin\\gradle javadoc'
      }
    }

    stage('Mail Notification') {
      steps {
        mail(cc: 'hk_bennamane@esi.dz', subject: 'build', body: 'new build')
      }
    }

    stage('Code Analysis') {
      parallel {
        stage('Code Analysis') {
          steps {
            withSonarQubeEnv('sonar') {
              bat 'D:\\SCHOOL\\SIL2\\S1\\done\\Outils\\TPs\\Gradle\\gradle-5.6\\bin\\gradle sonarqube'
            }
            script {
              echo "test SonarQube"
              def qg = waitForQualityGate()
              if (qg.status != 'OK') {
                error "pipline aborted due to quality gate failure :${qg.status}"
                echo "jjjjjjj"
              }
            }
          }
        }

        stage('Test reporting') {
          steps {
            cucumber 'reports/*.json'
          }
        }

      }
    }

    stage('Deployment') {
      steps {
        bat 'D:\\SCHOOL\\SIL2\\S1\\done\\Outils\\TPs\\Gradle\\gradle-5.6\\bin\\gradle publish'
      }
    }

    stage('Slack Notification') {
      steps {
        slackSend(baseUrl: 'https://hooks.slack.com/services/', channel: 'tp-jenkins', message: 'new build has been added', token: 'T01NG7VH880/B01S6APL8T1/SOREG7NXa4Ys3w3vcxBxXOBd', username: 'khadidja', teamDomain: 'Esi', color: '#008000')
      }
    }

  }
}
