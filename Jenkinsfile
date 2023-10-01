def resume_pipeline = true

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
            steps {
                echo 'Testing'
                ctest arguments:'-T test',installation: 'InSearchPath'
            }
            post {
                always {
                    archiveArtifacts artifacts: 'Testing/**/*.xml'
                    xunit([
                        CTest(pattern: 'Testing/**/*.xml')
                    ])

                    // xunit checksName:'',testTimeMargin: '3000'
                    //     thresholdMode: 1
                    //     thresholds: [
                    //     skipped(failureThreshold: '0')
                    //     failed(failureThreshold: '0')
                    //     ]
                }
            }        
        }
        stage('Deploy') {
            when {
                expression { abort_pipeline}
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