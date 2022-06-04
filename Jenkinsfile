System.setProperty('org.apache.commons.jelly.tags.fmt.timeZone', 'Asia/Shanghai');

def timeStamp = Calendar.getInstance().getTime().format('YYYYMMdd-hhmmss',TimeZone.getTimeZone('CST'))
println("timeStamp: ${timeStamp}")

String buildNumber = env.BUILD_NUMBER;
String timestamp = new Date().format('yyyy-MM-dd_HH-mm-ss', TimeZone.getTimeZone('Asia/Shanghai'));
String projectName = env.JOB_NAME.split(/\//)[0];
String version = "${buildNumber}_${timestamp}_${projectName}";

println("version: ${version}")

pipeline {
    agent {
        docker {
            image 'maven:3.8.1-adoptopenjdk-11'
            args '-v $HOME/.m2:/root/.m2'
            reuseNode true
        }
    }
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
                     customImage.push();
                     echo '🎉 Push Success 🎉'
                }
            }
        }
    }
}
