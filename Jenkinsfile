pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                // Pull latest code from your GitHub repo
                git branch: 'main', url: 'https://github.com/kondekarprajot/7-wonders-webapp.git'
            }
        }

        stage('Build WAR using Maven') {
            steps {
                // Clean and package your Maven project
                bat 'mvn clean package'
            }
        }

        stage('Deploy WAR to Tomcat') {
            steps {
                // Deploy WAR to Tomcat using Jenkins 'Deploy to container' plugin
                deploy adapters: [
                    tomcat9(
                        credentialsId: 'tomcat-credentials',  // Set this ID in Jenkins credentials
                        path: '', 
                        url: 'http://localhost:9090'          // Your Tomcat URL
                    )
                ], contextPath: '7wonders', war: '**/target/*.war'
            }
        }
    }

    post {
        success {
            echo '✅ Deployment Successful! Visit http://localhost:9090/7wonders'
        }
        failure {
            echo '❌ Build or Deployment Failed. Check console output for details.'
        }
    }
}
