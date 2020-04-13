pipeline{
	agent any

	stages {
	
	    stage('get build executer details') {
           steps {
               script {
                   wrap([$class: 'BuildUser']) {
                       echo "BUILD_USER_EMAIL=${BUILD_USER_EMAIL}"
                       echo "env.BUILD_USER_EMAIL=${env.BUILD_USER_EMAIL}"
                   }
               }
           }
       }
		stage('build'){
			parallel {
				stage('Build Master') {
					when {
						branch 'master'
					} 
					steps {    
						echo "Master Branch"
					}
					
			    post {
                success {
                    mail to: "kmitsie48@gmail.com", subject: 'The Pipeline Successed :)', body: 'Jenkins job triggered for other branch'
                }
            }
		}
				stage('Build 9.0.1') {
					when {
						branch '9.0.1'
					} 
					steps {
						echo "9.0.1 Branch"
					}
					
				post {
                success {
                    mail to: "kmitsie48@gmail.com", subject: 'The Pipeline Successed :)', body: 'Jenkins job triggered for other branch'
                }
            }
		}
				}
				stage('Build Branch') {
					when { 
						not {
							anyOf
							{
								branch 'master';
								branch '9.0.0';
								branch '9.0.1';
								branch '/^Feature.*$/'
							} 
						}
					}
					
				post {
                success {
                    mail to: "${env.BUILD_USER_EMAIL}", subject: 'The Pipeline Successed :)', body: 'Jenkins job triggered for other branch'
                }
				}
			}
		}
	}
}
