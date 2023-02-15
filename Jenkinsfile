pipeline {
    agent any
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
