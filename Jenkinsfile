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
                script{
                 def customImage = docker.build("pranav1303/petclinic:${env.BUILD_NUMBER}","./docker")
                  docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {


                 customImage.push()

            }
        }
        }
    }
    stage('kubernetes build'){
        steps{
            script{
                withKubeConfig([credentialsId: 'kubeconfig']) {
               sh 'pwd'
               sh 'cp -R helm/* .'
               sh 'ls -ltrh'
               sh '/usr/local/bin/helm upgrade --install petclinic-app petclinic --set image.repository=pranav1303/petclinic --set image.tag={env.BUILD_NUMBER}'   
    }
            }
        }
    }
}
}