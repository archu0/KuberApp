pipeline {
    agent any
    
    tools{
        maven 'maven'
    }

    stages {
        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage("Build image and push to dockerhub") {
            steps {
                script {
                    try {
                        sh "docker rmi archu09/kuberproject"
                        sh "docker rm marcos"
                    }
                    catch(err) {
                        echo err.getMessage()
                    }
                }
                sh '''  mv target/KuberApp.war .
                        docker build -t archu09/kuberproject .
                        docker login -u archu09 -p Archana09*
                        docker tag archu09/kuberproject archu09/kuberproject
                        docker push archu09/kuberproject
                    '''
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

