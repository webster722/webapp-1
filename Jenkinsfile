pipeline {
    agent any
    tools {
        maven 'maven'
    }
    environment {
        branch = 'master'
        scmUrl = 'https://github.com/webster722/webapp-1.git'
    }
    stages {
        stage('checkout git') {
            steps {
                git branch: branch, url: scmUrl
            }
        }

        stage('build') {
            steps {
                sh 'mvn clean package -DskipTests=true'
            }
        }

        stage ('test') {
            steps {
                parallel (
                    "unit tests": { sh 'mvn test' },
                    "integration tests": { sh 'mvn integration-test' }
                )
            }
        }
    }
}
