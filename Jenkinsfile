#!/usr/bin/env groovy
pipeline {
    agent any

    stages {
        stage('Dependencias') {
            steps {
                    sh 'yarn'

            }
        }
        stage('test') {
            steps {
                sh 'yarn run test'
            }
            post {
                always {
                    junit 'test/*-test.js'
                }
            }

        }
        stage('ci-test') {
            steps {
                sh 'yarn run ci-test'
            }
            post {
                always {
                    junit 'coverage/lcov-report/*.js'
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
