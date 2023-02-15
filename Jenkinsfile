pipeline {
    agent {
        node {
            label 'docker'
        }
    }
    stages {
        stage('test') {
            steps {
                withEnv(["HOME=${env.WORKSPACE}"]) {
                    echo "${env.SANDBOX_KONG_ADMIN}"
                }
            }
        }
    }
}
