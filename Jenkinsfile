pipeline {
    agent any
    tools {
        maven 'Maven-3.9.9'
    }
    stages {
        stage('git-clone') {
            steps {
                git 'https://github.com/vishal368/30-nov-maven-practice.git'
            }
        }
        stage('maven-build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('docker-image') {
            steps {
                sh "docker build . -t tomcatwebapp:${env.BUILD_ID}"
                sh 'docker tag tomcatwebapp:${env.BUILD_ID} vishashally/kubernate:05'
            }
        }
        stage('k8s deploy') {
            steps {
                sh 'kubectl apply -f k8s-deploy.yml'
            }
        }
    }
}
