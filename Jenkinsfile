pipeline {
    agent any
      environment {
        TOMCAT_SERVER = 'root@52.66.79.128'
        TOMCAT_DIR = '/root/apache-tomcat-9.0.98/webapps/'
        WAR_FILE = '/var/lib/jenkins/workspace/project/target/students.war'
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
                    sshagent([CREDENTIALS_ID]) {
                        sh """
                            scp -o StrictHostKeyChecking=no ${WAR_FILE} ${TOMCAT_SERVER}:${TOMCAT_DIR}
                            scp -r -o StrictHostKeyChecking=no ${APP_DIR} ${TOMCAT_SERVER}:${TOMCAT_DIR}
                        """
                    }
                }
            }
        }
    }
}
