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
            echo "CREDENTIALS_ID: ${CREDENTIALS_ID}"
            echo "WAR_FILE: ${WAR_FILE}"
            echo "TOMCAT_SERVER: ${TOMCAT_SERVER}"
            echo "TOMCAT_DIR: ${TOMCAT_DIR}"
            echo "APP_DIR: ${APP_DIR}"
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

