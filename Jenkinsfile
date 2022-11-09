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
                deploy adapters: [tomcat9(credentialsId: '39786a7b-87fb-4e08-b65b-7abf508731db', path: '', url: 'http://ec2-3-95-182-230.compute-1.amazonaws.com:8080')], contextPath: null, war: '**/*.war'
            }
        }
    }
}

