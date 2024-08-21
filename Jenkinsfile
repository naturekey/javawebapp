pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "Maven3.9.8"
    }

    stages {
	    stage('checkout'){
		 steps{
		 checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/naturekey/javawebapp.git']])
		 }
		}
		
        stage('Build') {
            steps {
                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
            stage('deploy to prod') {     
                 steps {
                    deploy adapters: [tomcat9(credentialsId: 'tomcat-server', path: '', url: 'http://172.31.95.230:8080/')], contextPath: null, war: '**/*.war'
                 }
        }
    }
}
