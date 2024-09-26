pipeline {
    agent any
    parameters {
        booleanParam(name: "RUN_INTEGRATION_TESTS", defaultValue: true)
    }
    stages {
        stage('Prepare') {
            steps {
                sh 'chmod +x ./mvnw'
            }
        }
        stage('Test') {
            parallel {
                stage('Unit Tests') {
                    steps {
                        sh './mvnw test -D testGroups=unit'
                    }
                }
                stage('Integration Tests') {
                    when { expression { params.RUN_INTEGRATION_TESTS } }
                    steps {
                        sh './mvnw test -D testGroups=integration'
                    }
                }
            }
        }
    }
}