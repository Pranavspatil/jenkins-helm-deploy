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
        stage ('Build Docker Image'){
            steps{
                script{
                    def customImage = docker.build("pranav1303/petclinic:${env.BUILD_NUMBER}", "./docker")
                      docker.withRegistry('https://registry.hub.docker.com', 'dockerhub'){
                         customImage.push()
                      }
                }
            }
        }
        stage('Build on Kubernatis'){
            steps{ 
                withKubeConfig([credentialsId: 'kubeconfig']){
                    sh 'pwd'
                    sh 'cp -r helm/*.'
                    sh 'ls -ltrh'
                    sh 'pwd'
                    sh '/usr/local/bin/helm upgrade --install petclinic-app petclinic --set image.repository=ashaik65/petclinic --set image.tag=${BUILD_NUMBER}'

                }

            }
        }
    }
}