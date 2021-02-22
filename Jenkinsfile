properties([
  buildDiscarder(logRotator(numToKeepStr: '5')),
  disableConcurrentBuilds()
])

timestamps() {
    timeout(time: 10, unit: 'MINUTES') {
        node {
            stage('Greeting') {
                withEnv(["JAVA_HOME=${tool 'jdk11'}", "PATH+MAVEN=${tool 'maven36'}/bin:${env.JAVA_HOME}/bin"]) {
                    sh "java -version"
                    sh "mvn --version"
                }
            }
        }
    }
}
