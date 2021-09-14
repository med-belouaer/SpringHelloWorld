pipeline {
    agent any

    stages {
        stage('Clone') {
            git 'https://github.com/med-belouaer/SpringHelloWorld.git'
          }
      
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test' 
            }
        }
        stage('Package') {
            steps {
                sh 'mvn package'
                sh 'docker build -t testspring:1 .'
            }
        }
        stage('Deploy') {
            steps {
              sh 'kubectl get pod'
              sh 'kubectl apply -f deployment.yaml'
              sh 'kubectl get pod'
            }
        }
    }
}

