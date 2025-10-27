pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/kondekarprajot/7-wonders-webapp.git'
            }
        }

        stage('Build WAR using Maven') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Deploy WAR to Tomcat') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'tomcat-credentials', usernameVariable: 'TOMCAT_USER', passwordVariable: 'TOMCAT_PASS')]) {
                    bat """
                        curl -T target/7-wonders-webapp-1.0.0.war "http://%TOMCAT_USER%:%TOMCAT_PASS%@localhost:9090/manager/text/deploy?path=/7wonders&update=true"
                    """
                }
            }
        }
    }

    post {
        success {
            echo '✅ Build and Deployment Successful!'
        }
        failure {
            echo '❌ Build or Deployment Failed. Check console output for details.'
        }
    }
}
