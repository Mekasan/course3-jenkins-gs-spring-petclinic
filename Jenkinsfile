    pipeline {
        agent any
            stages {

                stage("build") {
                    steps {
                        sh "./mvnw package"
                    }
                }

                stage("covarage") {
                    steps {
                        archiveArtifacts artifacts: '**/target/*.jar'
                        jacoco()
                        junit '**/target/surefire-reports/TEST*.xml'
                    }
                }
                stage("Run tests") {
                    steps {
                        sh './mvnw test'
                    }
                }
            }
            post {
                always {
                    slackSend(channel: "#jenkins", message: "${currentBuild. currentResult}: Job ${env.JOB_NAME} Build: ${env.BUILD_NUMBER} Link: ${env.BUILD_URL}")
                }
            }
        }
