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
            git{
                releaseVersion = '0.0.1'
            }
        }
    }
    stage ('signoff') {
        //def userInput = input(
          //  id: 'userInput', message: 'Let\'s promote?', parameters: [
          //  [$class: 'TextParameterDefinition']
        //])
        timeout(time:10, unit:'DAYS') {
            input message: "Does the application look good?"
        }
        node ()
        {
            echo "deploying to prod"
        }
    }
}
