def JOBNAME =  env.JOB_NAME.replaceFirst('.+/', '')

node () {
    stage('scm') {
        checkout scm
    }
    stage('run test') {
        echo 'testing'
    }

    if (JOBNAME == 'master') {
        stage('Deploy') {
            echo 'Deploying'
        }
    }
}
