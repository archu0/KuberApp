pipeline {
    agent any
      environment {
        TOMCAT_SERVER = 'root@52.66.204.22'
        TOMCAT_DIR = '/root/apache-tomcat-9.0.98/webapps/'
        WAR_FILE = '/var/lib/jenkins/workspace/kuberproject/target/KuberApp.war'
        APP_DIR = '/var/lib/jenkins/workspace/kuberproject/target/KuberApp'   
        CREDENTIALS_ID = 'ssh'  
    }
  
    tools{
        maven 'maven'
    }

    stages {
        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }
         stage('Transfer WAR to Tomcat') {
    steps {
        script {
            sshagent(['CREDENTIALS_ID']) {
                sh """
                    scp -o StrictHostKeyChecking=no ${WAR_FILE} ubuntu@${TOMCAT_SERVER}:${TOMCAT_DIR}
                    scp -r -o StrictHostKeyChecking=no ${APP_DIR} ubuntu@${TOMCAT_SERVER}:${TOMCAT_DIR}
                """
            }
        }
    }
}
    }


    post {
        success {
            echo 'Deployment successful'
        }
        failure {
            echo 'Deployment failed'
        }
    }
    }

