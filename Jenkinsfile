pipeline {
    agent any
    stages {
        stage('test') {
            steps {
                withEnv(["HOME=${env.WORKSPACE}"]) {
                    echo "${env.SANDBOX_KONG_ADMIN}"
                    echo "${env.WORKSPACE}"
                }
            }
        }
        stage('Artifactory push') {
            steps {
                rtServer (
                    id: "localArtifactory",
                    url: "http://172.17.0.21:8081",
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
                                    "target": "/artifactory/libs-release-local/test/1.0.0",
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
