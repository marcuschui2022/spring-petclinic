pipeline {
    agent any

    tools {
        maven 'Maven 3.9.6'
    }

    triggers {
        cron('H/10 * * * 1')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test and Generate Jacoco Report') {
            steps {
                sh 'mvn test jacoco:report'
            }
        }
    }

    post {
        always {
            //jacoco(execPattern: '**/*/target/site/jacoco/jacoco.xml')
            jacoco(
                execPattern: '**/**.exec',
                classPattern: '**/classes',
                sourcePattern: '**/src/main/java',
                changeBuildStatus: false
            )
        }
    }
}
