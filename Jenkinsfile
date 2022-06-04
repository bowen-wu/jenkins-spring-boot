def responseJson = new URL("http://101.35.43.9:5000/v2/test-jenkinsfile/tags/list")
        .getText(requestProperties: ['Content-Type': "application/json"]);

println(responseJson)

// {name:xxx,tags:[tag1,tag2,...]}
Map response = new groovy.json.JsonSlurperClassic().parseText(responseJson) as Map;

def versionsStr = response.tags.join('\n');

pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo "maven -v"
            }
        }
    }
}
