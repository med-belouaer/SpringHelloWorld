pipeline { 

    environment { 

        registry = "medbelouaer/testspring" 

        registryCredential = 'docker-hub-cred-med' 

        dockerImage = '' 

    }

    agent any 

    stages { 

        stage('Cloning our Git') { 

            steps { 

                git 'https://github.com/med-belouaer/SpringHelloWorld.git'
                sh 'mvn install test package'

            }

        } 

        stage('Building our image') { 

            steps { 

                script { 

                    //dockerImage = docker.build registry + ":$BUILD_NUMBER" 
                    dockerImage = docker.build registry + ":1"
                }

            } 

        }

        stage('Deploy image on docker hub') { 

            steps { 

                script { 

                    docker.withRegistry( '', registryCredential ) { 

                        dockerImage.push() 

                    }

                } 

            }

        } 

        stage('Cleaning up') { 

            steps { 

                sh "docker rmi $registry:1" 

            }

        }
        stage('Deploy on K8s') {
            steps {
                withKubeConfig([credentialsId: 'mykubeconfig']) {
                sh 'kubectl apply -f deployment.yaml'
                }
            }
        }

    }

}
