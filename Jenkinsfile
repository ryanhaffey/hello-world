def JOBNAME =  env.JOB_NAME.replaceFirst('.+/', '')


try {
    node () {
        stage('scm') {
            checkout scm
            sh 'git rev-parse --abbrev-ref HEAD > GIT_BRANCH'
            def git_branch = readFile('GIT_BRANCH').trim()
            echo "${git_branch}"

            sh 'git rev-parse HEAD > GIT_COMMIT'
            def git_commit = readFile('GIT_COMMIT').trim()
            echo "${git_commit}"
        }
        stage('run test') {
            echo 'testing'
        }
    }

    if (JOBNAME == 'master') {
        stage('Deploy') {
            node (){
                echo 'Deploying'
                // withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'ca9e3371-fbc4-4ed3-be39-f478266544fd', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME']]) {
                //     sh('git config --global user.email os-bot@onshift.com')
                //     sh('git config --global user.name os-bot')
                //     sh("git tag -a ${env.BUILD_NUMBER}_tag -m 'Jenkins'")
                //     sh('git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/ryanhaffey/hello-world.git --tags')
                // }
            }
        }
    }
}
catch (err){
    hipchatSend room: "CI-POC", token: "6wM31nsncn6Lcfm6DnsTIIX5rjFhXDGViZZpxnHa", message:"failed build"
}
