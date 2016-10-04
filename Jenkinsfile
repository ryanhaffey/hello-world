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
                sh("git tag -a ${env.BUILD_NUMBER}_tag -m 'Jenkins'")
                sh('git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/ryanhaffey/hello-world.git --tags')
            }
        }
    }
    stage ('signoff') {
        timeout(time:10, unit:'DAYS') {
            input message: "Does the application look good?"
        }
        node ()
        {
            hipchatSend message:"test message" token:6wM31nsncn6Lcfm6DnsTIIX5rjFhXDGViZZpxnHa room:CI-POC
            echo "deploying to prod"
        }
    }
}
