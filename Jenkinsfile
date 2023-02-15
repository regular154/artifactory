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
                    url: "http://172.17.0.2:8081/artifactory",
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
                                    "pattern": "${env.WORKSPACE}/*.md",
                                    "target": "/libs-release-local/1.0.0",
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
