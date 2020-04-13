pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo "Into Build stage"
	echo "BRANCH_NAME=${BRANCH_NAME}"
	echo "env.BRANCH_NAME=${env.BRANCH_NAME}"
      }
    }
  }
  post {
    always {
      deleteDir()
    }
  }
}
