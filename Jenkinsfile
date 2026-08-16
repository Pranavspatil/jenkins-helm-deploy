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
    }
}
