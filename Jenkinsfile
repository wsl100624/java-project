properties([pipelineTriggers([githubPush()])])

node('linux') {
    git url: 'https://github.com/wsl100624/java-project.git', branch: 'master'
    stage('Test') {
        sh "env"
    }
}
