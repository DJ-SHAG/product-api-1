pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                bat 'mvn clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Deployment to Exchange') {
            steps {
                bat 'mvn -s "C:/Users/rohan rana/.m2/settings.xml" clean deploy  -Pdev '
            }
        }
	stage('Deployment to Anypoint Runtime') {
            steps {
                bat 'mvn -s "C:/Users/rohan rana/.m2/settings.xml" clean deploy  -Pdev -DmuleDeploy '
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