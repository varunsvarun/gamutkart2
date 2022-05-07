pipeline {
    agent any

//	tools {
//		maven 'maven3.6'
//	}
//	environment {
//		M2_INSTALL = "/usr/bin/mvn"
//	}

    stages {
        stage('Clone-Repo') {
	    steps {
	        checkout scm
	    }
        }

        stage('Build') {
            steps {
                sh 'mvn install -Dmaven.test.skip=true'
            }
        }
		
        stage('Unit Tests') {
            steps {
                sh 'mvn compiler:testCompile'
                sh 'mvn surefire:test'
                junit 'target/**/*.xml'
            }
        }

        stage('Deployment') {
            steps {
                sh 'sshpass -p "123" -v scp target/gamutgurus.war varun@172.17.0.3:/home/varun/Distros/apache-tomcat-9.0.59/webapps'
                sh 'sshpass -p "123" -v ssh varun@172.17.0.3 "/home/varun/Distros/apache-tomcat-9.0.59/bin/startup.sh"'
            }
        }
    }
}
