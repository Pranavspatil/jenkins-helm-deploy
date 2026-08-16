pipeline{
    agent any

    stages{
        stage('build maven'){
            steps{
                sh 'pwd'
                sh 'mvn clean install package'
                echo 'maven all packages are installed'
            }
        }
        stage('copy'){
            steps{
                sh 'pwd'
                sh 'cp -r target/*.jar docker/'
            }
        }
        stage('test'){
            steps{
                sh 'mvn test'

            }
        }
        stage('build docker image'){
            steps{
                 def customImage = docker.build("pranav1303/petclinic:${env.BUILD_NUMBER}")
                  docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {


                 customImage.push()

            }
        }
    }
}
}