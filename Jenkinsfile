pipeline {
    agent {
        kubernetes {
            label 'maven_build'
            defaultContainer 'jnlp'
            yaml """
apiVersion: v1
kind: Pod
metadata:
  labels:
    some-label: some-label-value
spec:
  containers:
  - name: maven
    image: maven:alpine
    command:
    - cat
    tty: true
"""
        }
    }
    stages {
        stage('Run maven build') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'acr_login', passwordVariable: 'key', usernameVariable: 'application_id')]) {
                    container('maven') {
                        sh 'mvn -version'
                        sh 'mvn package'
                    }
                }

            }
        }
    }
}
