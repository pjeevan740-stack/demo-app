pipeline {
    agent any

    tools {
        maven 'Maven'
        jdk 'JDK21'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url:'https://github.com/Naveen04jan/ven.git', 
                credentialsId: 'github-token'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Run Application') {
            steps {
                sh 'mvn exec:java -Dexec.mainClass="com.example.app.App"'
            }
        }
    }

    /* --- ADDED POST SECTION --- */
    post {
        success {
            emailext(
                 subject: "Success: Pipeline ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                 body: "The build was successful. View the details here: ${env.BUILD_URL}"
                 to:"pjeevan740@gmail.com"
                )
        }
        failure {
            emailext(
                 subject: "Failed: Pipeline ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                 body: "The build failed. Check the logs at: ${env.BUILD_URL}"
                 to:"pjeevan740@gmail.com"
                )
        }
    }
}
