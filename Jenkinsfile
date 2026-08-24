pipeline {
    agent any
	environment {
		ANYPOINT_CREDS = credentials('ANYPOINT_CREDENTIALS')
	
	}

    stages {

        stage('Build') {
            steps {
                bat 'mvn clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                echo 'mvn test'
            }
        }

        stage('Deployment to Exchange') {
			environment {
				CLIENT_ID = credentials('DEV_CLIENT_ID')
				Client_SECRET = credentials('DEV_CLIENT_SECRET')
				
			}
            steps {
                bat 'mvn -s "C:/Users/rohan rana/.m2/settings.xml"  clean deploy  -Pdev -Dusername="%ANYPOINT_CREDS_USR%" -Dpassword="%ANYPOINT_CREDS_PSW%" -Danypoint.platform.client_id="%CLIENT_ID%" -Danypoint.platform.client_secret="%Client_SECRET%"'
            }
        }
	stage('Deployment to Anypoint Runtime') {
			environment {
				CLIENT_ID = credentials('DEV_CLIENT_ID')
				Client_SECRET = credentials('DEV_CLIENT_SECRET')
				
			}
            steps {
                bat 'mvn -s "C:/Users/rohan rana/.m2/settings.xml"  clean deploy  -Pdev -DmuleDeploy -Dusername="%ANYPOINT_CREDS_USR%" -Dpassword="%ANYPOINT_CREDS_PSW%" -Danypoint.platform.client_id="%CLIENT_ID%" -Danypoint.platform.client_secret="%Client_SECRET%" '
            }
        }
    }

    post {
        success {
            echo 'Build, Test and Deployment completed successfully.'
        }

        failure {
            echo 'Pipeline failed.'
        }
    }
}