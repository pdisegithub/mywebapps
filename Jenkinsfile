pipeline {
    agent any
    tools {
    maven 'Maven3.8.4'	
	}
    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/keyspaceits/javawebapp.git']]])
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean install -f pom.xml'
            }
        }
        stage('Deploy to Tomcat') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'tomcat-deployer', path: '', url: 'http://192.168.1.36/')], contextPath: null, war: '**/*.war'
            }
        }
    }
}

