pipeline {
    agent {
        dockerfile {
            filename 'Dockerfile'
            dir 'dev'
        }
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building'
                sh "cmake . && make"
            }
        }
        stage('Test') {
            steps {
                echo 'Testing'
                sh "make test"
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying'
            }
        }
    }
}