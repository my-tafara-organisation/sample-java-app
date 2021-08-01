pipeline {
	agent NONE

	triggers {
		pollSCM '* * * * *'
	}


	stages{
	
	    stage('Fetch Code') {
                steps {
                    git branch: 'main', url: 'https://github.com/my-tafara-organisation/sample-java-app.git'
                }
            }
        
            stage('BUILD'){
                steps {
                    sh 'mvn clean install -DskipTests'
                }
                post {
                    success {
                        echo 'Now Archiving...'
                      //  archiveArtifacts artifacts: '**/*.war'
                    }
                }
            }
        
            stage('UNIT TEST'){
                steps {
                    sh 'mvn test'
                }
            }
        
            stage('INTEGRATION TEST'){
                steps {
                    sh 'mvn verify -DskipUnitTests'
                }
            }
        
            stage ('CODE ANALYSIS WITH CHECKSTYLE'){
                steps {
                    sh 'mvn checkstyle:checkstyle'
                }
                post {
                    success {
                        echo 'Generated Analysis Result'
                    }
                }
            }
        }
}
        
