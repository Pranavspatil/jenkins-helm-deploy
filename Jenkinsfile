pipeline {
    agent any
    stages{
        stage('build maven') {
            steps{
                sh 'pwd'
                sh 'mvn clean install package'
            }
        }
        stage('Copy Artifact'){
            steps{
                sh 'pwd'
                sh 'cp -r target/*.jar docker'
            }
        }
        stage('Unit Test'){
            steps{
                sh 'mvn test'
            }
        }
        stage{
            steps{
                script{
                    def customImage = docker.build("pranav1303/petclinic:${env.BUILD_NUMBER}", "./docker")
                      docker.withRegistry('https://registry.hub.com', 'dockerhub'){
                         customImage.push()
                      }
                }
            }
        }
    }
}