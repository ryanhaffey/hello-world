def JOBNAME =  env.JOB_NAME.replaceFirst('.+/', '')

node () {
    stage('scm') {
        checkout scm
    }
    stage('run test') {
        echo 'testing'
    }
}

if (JOBNAME == 'master') {
    stage('Deploy') {
        node (){
            echo 'Deploying'
        }
    }
    stage ('signoff') {
        def userInput = input(
            id: 'userInput', message: 'Let\'s promote?', parameters: [
            [$class: 'TextParameterDefinition']
        ])
        node ()
        {
            echo ("User Input: "+userInput)
        }
    }
}
