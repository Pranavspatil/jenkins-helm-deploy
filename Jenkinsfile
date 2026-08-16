pipeline{
    agent any

    stages{
        stage('build maven'){
            steps{
                sh 'pwd'
                sh 'mvn clean installl package'
            }
        }
    }
}
