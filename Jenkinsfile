pipeline {
    agent any
    tools {
        maven 'MAVEN-3.9.9'
        jdk 'JDK17'
    }
	
    stages {
		stage('show_variables') {
			steps {
				echo "Build ID        = ${env.BUILD_ID}"
                echo "Build Number    = ${env.BUILD_NUMBER}"
                echo "Build Tag       = ${env.BUILD_TAG}"
                echo "Build URL       = ${env.BUILD_URL}"
                echo "Executor Number = ${env.EXECUTOR_NUMBER}"
                echo "Java Home       = ${env.JAVA_HOME}"
                echo "Jenkins URL     = ${env.JENKINS_URL}"
                echo "Job Name        = ${env.JOB_NAME}"
                echo "Node Name       = ${env.NODE_NAME}"
                echo "Workspace       = ${env.WORKSPACE}"
			}
		}
        stage('Checkout') {
            steps {
                git branch:'main', url:'https://github.com/amolpate/jenkin-webapp.git'
            }
        }
        stage('build') {
            steps {
                bat "mvn clean package -f jenkin/pom.xml"
            }
        }
    }
}