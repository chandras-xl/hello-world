pipeline{
    agent any
    environment{
        HOME = "/home/ubuntu/artifact"
    }
    stages{
        stage('Build'){
            steps{
                sh 'mvn clean install package'
            }
        }
        stage('Copy artifacts'){
            steps{
                sh "cp webapp/target/*.war ${env.HOME}"
            }
        }
        stage('Docker build'){
            steps{
                sh "docker build ${env.HOME}/."
                sh "docker images"
            }
        }
        // stage("Run docker container"){
        //     steps{
        //         sh "docker run -d "
        //     }
        // }
    }
    post{
        always{
            cleanWs()
        }
        success{
            slackSend channel: '#jenkinsci',
                      color: 'good',
                      message: "Successfully executed ${currentBuild.fullDisplayName}"
        }
        failure{
            slackSend channel: '#jenkinsci',
                      color: 'danger',
                      message: "Failed to execute ${currentBuild.fullDisplayName}"
        }
    }
}