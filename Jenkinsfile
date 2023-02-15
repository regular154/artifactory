pipeline {
    agent any
    stages {
        stage('test') {
            steps {                
                echo "${env.SANDBOX_KONG_ADMIN}"
                echo "${env.WORKSPACE}"
                sh "pwd"
                sh "ls"
            }
        }
        stage('Artifactory push') {
            steps {
                rtBuildInfo (
                    captureEnv: true
                )
                rtUpload (
                    serverId: "my-jfrog-instance",
                        spec: """{
                            "files": [
                                {
                                    "pattern": "*.md",
                                    "target": "/generic/test/100/",
                                    "props": "vcs.repository=testValue"  
                                }
                            ]
                        }"""
                )
                rtPublishBuildInfo (
                    serverId: "my-jfrog-instance"
                )
            }
        }
    }
}
