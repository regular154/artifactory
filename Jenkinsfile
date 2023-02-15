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
                rtServer (
                    id: "localArtifactory",
                    url: "http://172.17.0.2:8081",
                    credentialsId: "my-jfrog-credentials",
                    timeout: 300
                )
                rtBuildInfo (
                    captureEnv: true
                )
                rtUpload (
                    serverId: "localArtifactory",
                        spec: """{
                            "files": [
                                {
                                    "pattern": "*.md",
                                    "target": "/artifactory/libs-release-local/test/100/",
                                    "props": "vcs.repository=testValue",
                                    "flat": "true",
                                    "recursive": "true"
                                }
                            ]
                        }"""
                )
                rtPublishBuildInfo (
                    serverId: "localArtifactory"
                )
            }
        }
    }
}
