properties([
    buildDiscarder(logRotator(numToKeepStr: '5')),
    parameters([string(defaultValue: 'Jenkins Techlab', description: 'Who to greet?', name: 'Greetings_to')])
])

timestamps() {
    timeout(time: 10, unit: 'MINUTES') {
        node {
            stage('Greeting') {
                echo 'Hello, ' + params.Greetings_to + '!'
            }
        }
    }
}
