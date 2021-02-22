properties([
  buildDiscarder(logRotator(numToKeepStr: '5')),
  disableConcurrentBuilds()
])

try {
    timestamps() {
        timeout(time: 10, unit: 'MINUTES') {
            node {
                stage('Build') {
                    try {
                        withEnv(["JAVA_HOME=${tool 'jdk11'}", "PATH+MAVEN=${tool 'maven36'}/bin:${env.JAVA_HOME}/bin"]) {
                            checkout scm
                            sh 'mvn -B -V -U -e clean verify -Dsurefire.useFile=false -DargLine="-Djdk.net.URLClassPath.disableClassPathURLCheck=true"'
                            archiveArtifacts 'target/*.?ar'
                        }
                    } finally {
                        junit 'target/**/*.xml'  // Requires JUnit plugin
                    }
                }
            }
        }
    }
} catch (e) {
    node {
        rocketSend avatar: 'https://chat.puzzle.ch/emoji-custom/failure.png',  message: "Build failure - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)", rawMessage: true
    }
    throw e
} finally {
    node {
        if (currentBuild.result == 'UNSTABLE') {
             rocketSend avatar: 'https://chat.puzzle.ch/emoji-custom/unstable.png',  message: "Build unstable - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)", rawMessage: true
        } else if (currentBuild.result == null) { // null means success
            rocketSend avatar: 'https://chat.puzzle.ch/emoji-custom/success.png',  message: "Build success - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)", rawMessage: true
        }
    }
}
