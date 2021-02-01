#!/usr/bin/env groovy
pipeline {
    agent any
    tools {
        node 'v14.15.4'
    }

    stages {
        stage('Dependencias') {
            steps {
                    sh 'yarn'

            }
        }
        stage('test') {
            steps {
                sh 'npm install -g tap-junit'
                sh 'yarn run test | ./node_modules/tap-junit/bin/tap-junit --output output/test'
        
            }
            post {
                always {
                    junit 'output/test/*.xml'
                }
            }

        }
        stage('ci-test') {
            steps {
                sh 'yarn run ci-test| ./node_modules/tap-junit/bin/tap-junit --output output/ci-test'
            }
            post {
                always {
                    junit 'output/ci-test/*.xml'
                }
            }

        }
        stage('Build-jacoco') {
            steps {
                step([$class: 'JacocoPublisher', 
                    execPattern: 'build/jacoco/*.exec',
                    classPattern: 'build/classes',
                    sourcePattern: 'src/main/java',
                    exclusionPattern: 'src/test*'
                    ])
            }
        }
        
    }
}
