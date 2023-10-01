pipeline {
    agent {
        dockerfile {
            filename 'Dockerfile'
            dir 'dev'
        }
    }
	parameters {
		booleanParam name: 'RUN_TESTS', defaultValue: true, description: 'Run Tests?'
		booleanParam name: 'DEPLOY', defaultValue: true, description: 'Deploy Artifacts?'
	}
    stages {
        stage('Build') {
            steps {
                echo 'Building'
                sh "cmake . && make"
            }
        }
        stage('Test') {
            when {
                environment name: 'RUN_TESTS', value: 'true'
            }
            steps {
                echo 'Testing'
                sh "make test"
            }
        }
        stage('Deploy') {
            when {
                environment name: 'DEPLOY', value: 'true'
            }
            steps {
                echo 'Deploying'
            }
        }
    }
}