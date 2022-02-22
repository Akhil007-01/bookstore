#!/usr/bin/env groovy
def STATUS = ['SUCCESS': 'good', 'FAILURE': 'danger', 'UNSTABLE': 'danger', 'ABORTED': 'danger']

pipeline{
    agent any
    stages{
        stage('Building the app using maven') {
            steps {
                sh '''
                echo building the maven application
                export M2_HOME=/usr/local/apache-maven
                export M2=$M2_HOME/bin
                export PATH=$M2:$PATH
                mvn clean install
                '''
            }
        }
        stage('Building the docker image') {
            steps {
                sh '''
                docker build . -t bookstore:${BUILD_NUMBER}
                '''
            }
        }
        stage('Pushing to docker hub') {
            steps {
                sh '''
                docker tag bookstore:${BUILD_NUMBER} akhil37/bookstore:${BUILD_NUMBER}
                docker login -u akhil37 -p Akhil@7421
                docker push akhil37/bookstore:${BUILD_NUMBER}
                '''
            }
        }
    }    
}
