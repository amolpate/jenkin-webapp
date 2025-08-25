pipeline {
    agent any
    tools {
        maven 'MAVEN-3.9.10'
        jdk 'JDK17'
    }
	
	environment {
		APP_NAME   = "JenkinWebApp"
        APP_PORT   = "9090"
        DEPLOY_DIR = "jenkin/target"
	}
	
	parameters {
		string(name:'MODULE', defaultValue:'LOS', description:'Loan Origination Management')
		choice(name:'MODULE_TYPE', choices:['LOS','LMS','Collection'], description: 'Select module type')
		booleanParam(name:'DEBUG_MODE', defaultValue:false, description:'Enable debug logs?')
	}
	
	triggers {
		// (MINUTE   HOUR   DAY_OF_MONTH   MONTH   DAY_OF_WEEK) 
		cron('H/5 * * * *')	// Every 5 minute
		cron('H * * * *')	// Every hour
		cron('H 2 * * *')	// Every day at 2 AM
		cron('H 2 * * 1')	// Every Monday at 2 AM
		cron('H 0 * * *')	// Every day at midnight (12 AM)
		cron('H 12 * * 0')	// Every Sunday at 12 PM (noon)
		cron('H 9 1 * *')	// 9 AM on 1st of every month
		cron('H 9 * * 1-5')	// only weekdays at 9 AM
		cron('H 0 */2 * * *')	// Every 2 hours
		cron('H/30 8-18 * * 1-5')	// Every 30 minutes between 8 AM–6 PM, Monday–Friday
	}
	
    stages {
		stage('show_parameteres') {
			steps {
				echo "Module Name: ${params.MODULE}"
				echo "Module Type Name: ${params.MODULE_TYPE}"
				echo "Debug Mode Name: ${params.DEBUG_MODE}"
			}
		}
		stage('show_variables') {
			steps {
				echo "***** Jenkins built-in environment variables *****"
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
				echo "***** Setting environment variables *****"
                echo "Workspace       = ${env.APP_NAME}"
                echo "Workspace       = ${env.APP_PORT}"
                echo "Workspace       = ${env.DEPLOY_DIR}"
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
	
	post {
		always {
			echo "SCM pipeline handling POC success"
		}
		failure {
			echo "SCM pipeline handling POC fail"
		}
	}
}
