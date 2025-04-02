void setBuildStatus(String message, String state) {
    step([
        $class: "GitHubCommitStatusSetter",
        reposSource: [$class: "ManuallyEnteredRepositorySource", url: "https://github.com/my-org/my-repo"],
        contextSource: [$class: "ManuallyEnteredCommitContextSource", context: "ci/jenkins/build-status"],
        errorHandlers: [[$class: "ChangingBuildStatusErrorHandler", result: "UNSTABLE"]],
        statusResultSource: [ $class: "ConditionalStatusResultSource", results: [[$class: "AnyBuildResult", message: message, state: state]] ]
    ]);
}

pipeline {
    agent any

    stages {
        stage('Initialize') {
            steps {
                script {
                    setBuildStatus("Build start", "PENDING")
                }
            }
        }

        stage('Build') {
            steps {
                echo "Building.."
                sh '''
                    echo "doing build stuff.."
                '''
            }
        }

        stage('Test') {
            steps {
                echo "Testing.."
                sh '''
                    echo "doing test stuff.."
                '''
            }
        }

        stage('Deliver') {
            steps {
                echo "Deliver...."
                sh '''
                    echo "doing delivery stuff.."
                '''
            }
        }
    }

    post {
        success {
            script {
                setBuildStatus("Build complete", "SUCCESS")
            }
        }
        failure {
            script {
                setBuildStatus("Build failed", "FAILURE")
            }
        }
    }
}
