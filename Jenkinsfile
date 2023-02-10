pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    stages {
        stage('build jar') {
            steps {
                script {
                    echo "Building the application"
                    sh 'mvn package'
                }
            }
        }
        stage('build image') {
            steps {
                script {
                    echo "Building docker image" 
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-repo',passwordVariable:'DOCKERPASS',usernameVariable: 'DOCKERUSR')]) {
                        sh 'docker build -t zikou/maven-app:1.0 .'
                        sh "echo $DOCKERPASS | docker login -u $DOCKERUSR --password-stdin"
                        sh "docker push zikou/maven-app:1.0"
                    }
                }
            }
        }
        stage("deploy") {
            steps {
                script {
                    echo "Deploy the application"
                }
            }
        }
    }
        
}
