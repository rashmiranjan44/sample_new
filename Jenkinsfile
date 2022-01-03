pipeline {
    
    agent any

    options {
	    disableConcurrentBuilds()
	}
	
    stages {

        stage("Checkout Scm") {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '**']], extensions: [], 
                          userRemoteConfigs: [[url: 'https://github.com/rashmiranjan44/sample_new.git']]])
            }
        }
		
		stage("Build") {
            steps {
                sh "mvn clean compile"
            }
        }

        stage("Package") {
            steps {
                sh "mvn clean package"
            }
        }
		
		stage("Deploy") {
            steps {
                sh "cp /var/lib/jenkins/workspace/greyamp_pipeline/target/sparkjava-hello-world-1.0.war /root/tomcat/webapps"
                sh "export JRE_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.312.b07-1.amzn2.0.2.x86_64/jre"
                sh "export CATALINA_HOME=/root/tomcat"
                sh "cd /root/tomcat/bin && ./catalina.sh start"
                sh "cd /root/tomcat/bin && ./catalina.sh stop"
                sh "cd /root/tomcat/bin && ./catalina.sh start"
            }
        }
    }
}
