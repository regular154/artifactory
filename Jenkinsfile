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
        stage('Artifactory push') {
            steps {
                rtServer (
                    id: "localArtifactory",
                    url: "http://localhost:8082/artifactory",
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
                                    "pattern": "${WORKSPACE}/*.md",
                                    "target": "/libs-release-local/com/testproj/1.0.0",
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
