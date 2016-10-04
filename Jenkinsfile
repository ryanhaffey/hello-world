node () {
    stage('scm') {
        checkout scm
        echo env.JOB_NAME
        echo env.JOB_NAME.replaceFirst('.+/', '')
    }
    stage('run test') {
        echo 'testing'
    }
}
