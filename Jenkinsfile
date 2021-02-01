#!/usr/bin/env groovy
pipeline {
    agent any}

    stages {
        stage('Dependencias') {
            steps {
                    sh 'yarn'
                }
            }
        }
        stage('test') {
            steps {
                sh 'yarn run test'
            }
        }
        stage('ci-test') {
            steps {
                sh 'yarn run ci-test'
            }
        }
        
    }
}
