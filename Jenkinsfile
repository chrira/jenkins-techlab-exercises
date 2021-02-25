pipeline {
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
        timeout(time: 10, unit: 'MINUTES')
        timestamps()  // Timestamper Plugin
        disableConcurrentBuilds()
    }
    stages {
        stage('Build') {
            steps {
                sh "docker build -t gitlab.puzzle.ch/testimage/image:latest ."
            }
        }
    }
}
