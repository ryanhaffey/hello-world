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
            withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'ca9e3371-fbc4-4ed3-be39-f478266544fd', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME']]) {
                sh('git config --global user.email os-bot@onshift.com')
                sh('git config --global user.name os-bot')
                sh("git tag -a some_tag -m 'Jenkins'")
                sh('git push https://${GIT_USERNAME}:${GIT_PASSWORD}@https://github.com/ryanhaffey/hello-world.git --tags')
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
