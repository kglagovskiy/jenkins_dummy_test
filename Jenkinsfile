pipeline {
    agent {
        dockerfile {
            filename 'Dockerfile'
            dir 'dev'
        }
    }
    environment {
        EMAIL_TO = 'allerill@gmail.com'
    }
	parameters {
		booleanParam name: 'RUN_TESTS', defaultValue: true, description: 'Run Tests?'
		booleanParam name: 'DEPLOY', defaultValue: true, description: 'Deploy Artifacts?'
	}
    stages {
        stage('Build') {
            steps {
                echo 'Building'
                cmakeBuild installation: 'InSearchPath'
            }
            post {
                failure {
                    emailext body: 'Building failed', 
                        to: "${EMAIL_TO}", 
                        subject: 'Building failed'
                }
            }
        }
        stage('Test') {
            when {
                parameters name: 'RUN_TESTS', value: 'true'
            }
            steps {
                echo 'Testing'
                ctest installation: 'InSearchPath' 
                    arguments: '--output-junit test.xml'
            }
            // post {
            //     always {
            //         junit(
            //             allowEmptyResults: true,
            //             testResults: '**/test-reports/*.xml'
            //         )
            //     }
            // }        
        }
        stage('Deploy') {
            when {
                parameters name: 'DEPLOY', value: 'true'
            }
            steps {
                echo 'Deploying'
            }
            post {
                success {
                    emailext body: 'Deploying completed\n Congratulations !', 
                        to: "${EMAIL_TO}", 
                        subject: 'Deploying completed'
                }
            }  
        }
    }
}