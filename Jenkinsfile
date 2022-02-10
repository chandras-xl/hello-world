pipeline{
    agent any

    stages{
        stage('Build'){
            steps{
                sh 'mvn clean install package'
            }
        }
        stage('Copy artifacts'){
            steps{
                sh '''
                    cp webapp/target/*.war /home/ubuntu/artifact
                '''
            }
        }
    }
    post{
        // always{
        //     cleanWs()
        // }
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