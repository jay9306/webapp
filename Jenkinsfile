pipeline {
    agent any

    stages {
        stage('Check-out') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/jay9306/webapp']]])
            }
        }
        
        stage ('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        
        stage ('jacoco') {
            steps {
                jacoco()
            }
        }
        
        stage ('deploy') {
            steps {
                deploy adapters: [tomcat9(credentialsId: '7a96a5b4-e757-4257-aed0-fb0f80c6ed55', path: '', url: 'http://ec2-54-175-180-184.compute-1.amazonaws.com:8080')], contextPath: null, war: '**/*.war'
            }
        }
    }
}
