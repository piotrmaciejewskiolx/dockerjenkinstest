pipeline {
    agent any
    stages {
        stage('Build test image') {
            steps {
                sh 'docker build -f ./Dockerfile.test -t "dockerstack:test" .'
            }
        }

        stage('Unit tests') {
            steps {
                sh 'docker run --rm dockerstack:test vendor/bin/phpunit'
            }
        }
     }
}