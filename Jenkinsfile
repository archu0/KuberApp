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
                        sh "docker rmi sam"
                        sh "docker rm marcos"
                    }
                    catch(err) {
                        echo err.getMessage()
                    }
                }
                sh '''  mv target/KuberApp.war .
                        docker build -t sam .
                        docker login -u archu09 -p Archana09*
                        docker tag sam archu09/kuberproject
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

