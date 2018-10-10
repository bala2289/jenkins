#!/usr/bin/env groovy
pipeline {
    agent any
    stages {
        stage('pipeline start') {
            steps {
                sh 'echo "pipeline initiated.."'
            }
        }
        stage('build docker image') {
            steps {
                sh 'git clone https://github.com/bala2289/website-counter.git'
                sh 'cd website-counter'
                sh  builddate=`date +"%m-%d-%y-%H-%M"`
                sh 'docker build -t website-counter:$builddate .'
                sh 'docker tag website-counter:$builddate bala2289/website-counter:$builddate'
                }
        }
        stage('docker push') {
            steps {
                sh 'docker login --username bala2289 -p 1AmAwesome2289!dh'
                sh 'docker push website-counter'
            }
        }
    
    post { 
        always { 
            echo 'Cleaning up..'
            sh 'docker rmi website-counter'
        }
    }
}