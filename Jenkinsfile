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
						branch "master"
					} 
					steps {    
						mail to: "kmitsie48@gmail.com", subject: 'The Pipeline Successed :)', body: 'Jenkins job triggered for master branch'
					}
				}
				stage('Build 9.0.1') {
					when {
						branch "9.0.1"
					} 
					steps {
						mail to: "kmitsie48@gmail.com", subject: 'The Pipeline Successed :)', body: 'Jenkins job triggered for 9.0.1 branch'
					}
				}
				stage('Build Branch') {
					when { 
						not {
							anyOf
							{
								branch "master";
								branch "9.0.0";
								branch "9.0.1";
								branch "/^Feature.*\$/"
							} 
						}
					} 
					steps {
						mail to: "${env.BUILD_USER_EMAIL}", subject: 'The Pipeline Successed :)', body: 'Jenkins job triggered for other branch'
					}
				}
			}
		}
	}
}
