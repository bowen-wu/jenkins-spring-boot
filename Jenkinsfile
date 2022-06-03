pipeline {
    agent any
    triggers {
       pollSCM('* * * * *')
    }
    stages {
        stage('Test') {
            agent {
                docker { image 'circleci/openjdk:8u212-jdk-stretch' }
            }
            steps {
                sh 'mvn clean verify'
                echo '🎉 Verify Success 🎉'
            }
        }
        stage('Docker Build') {
            steps {
                echo 'Starting to build docker image'

                script {
                     def customImage = docker.build("101.35.43.9:5000/test-jenkinsfile:${new Date().format('yyyy-MM-dd_HH-mm-ss')}")
                     echo '🎉 Docker Build Success 🎉'
                }
            }
        }
    }
}
