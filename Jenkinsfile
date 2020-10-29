pipeline {
	agent any
	environment {
        JAVA_HOME = $(/usr/lib/jvm/java-8-openjdk-amd64)
        PATH = $JAVA_HOME/jre/bin:$PATH
    	}
	stages {
		stage('Checkout SCM') {
			steps {
				git 'https://github.com/owentoh/test.git'
			}
		}

		stage('OWASP DependencyCheck') {
			steps {
				dependencyCheck additionalArguments: '--format HTML --format XML', odcInstallation: 'Default'
			}
		}
	}	
	post {
		success {
			dependencyCheckPublisher pattern: 'dependency-check-report.xml'
		}
	}
}
