node {

        stage('Clone') {
            git ' https://github.com/med-belouaer/SpringHelloWorld.git'
          }
      
        stage('Build') {
            
                sh 'mvn install test package'
            
        }
        stage('Test') {
            
                sh 'mvn test' 
            
        }
        stage('Package') {
            
                sh 'mvn package'
                sh 'docker build -t testspring:1 .'
            
        }
        stage('Deploy') {
         
              sh 'kubectl get pod'
              sh 'kubectl apply -f deployment.yaml'
              sh 'kubectl get pod'
            
        }
    
}

