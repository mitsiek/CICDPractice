pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo "Into Build stage"
      }
    }
  }
  post {
    always {
      deleteDir()
    }
    success {
      script {
        if (env.BRANCH_NAME == 'origin/master') {
          emailext (
            to: 'kmitsie48@gmail.com',
            subject: "${env.JOB_NAME} #${env.BUILD_NUMBER} master is fine",
            body: "The master build is happy.\n\nConsole: ${env.BUILD_URL}.\n\n",
            attachLog: true,
          )
        } else if (env.BRANCH_NAME == 'origin/development') {
          // also send email to tell people their PR status
		  emailext (
            to: 'kmitsie48@gmail.com',
            subject: "${env.JOB_NAME} #${env.BUILD_NUMBER} development is fine",
            body: "The development build is happy.\n\nConsole: ${env.BUILD_URL}.\n\n",
            attachLog: true,
          )
        } else {
          // this is some other branch
		  emailext (
            to: 'miteshkokare21@gmail.com',
            subject: "${env.JOB_NAME} #${env.BUILD_NUMBER} production is fine",
            body: "The production build is happy.\n\nConsole: ${env.BUILD_URL}.\n\n",
            attachLog: true,
          )
        } 
      }
    }     
  }
}
