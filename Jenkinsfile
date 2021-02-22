properties([
  buildDiscarder(logRotator(numToKeepStr: '5')),
  disableConcurrentBuilds()
])

timestamps() {
    timeout(time: 10, unit: 'MINUTES') {
        node {
            stage('Greeting') {
                echo 'Hello, World!'
            }
        }
    }
}
