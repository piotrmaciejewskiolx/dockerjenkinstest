pipeline {
    agent any
    parameters {
           booleanParam(name: 'staging', defaultValue: false, description: 'Build and deploy to staging environment')
           booleanParam(name: 'production', defaultValue: false, description: 'Build and deploy to production environment')
    }
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
     stage('Build staging image') {
         when {
             expression {
                 env.BRANCH_NAME == 'master' && params.staging == true
             }
         }
         steps {
             sh 'docker build -f "Dockerfile.test" -t "dockerstack:staging" .'
         }
     }
}