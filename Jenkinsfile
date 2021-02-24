pipeline {
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
        timeout(time: 10, unit: 'MINUTES')
        timestamps()  // Timestamper Plugin
        disableConcurrentBuilds()
    }
    tools {
        oc 'oc4'
    }
    environment {
        APP_LABEL = 'my-app'
        OPENSHIFT_PROJECT = 'craaflaub-amm-test'
    }
    stages {
        stage('oc test') {
            steps {
                println "PATH: ${PATH}"

                println "OC Version from Shell, must be available:"
                sh "oc version"

                println "which oc"
                sh "which oc"
            }
        }
        stage('oc login') {
            steps {
                script {
                    openshift.withCluster("my-cluster") {
                        openshift.withCredentials("openshift-jenkins-external") {
                            openshift.withProject(env.OPENSHIFT_PROJECT) {
                                println "OC Version from Plugin:"
                                println openshift.raw('version').out
                                echo "Hello from project ${openshift.project()} in cluster ${openshift.cluster()}"
                                println openshift.raw('get','project').out
                                println openshift.raw('status').out
                                println openshift.raw('get','pod').out
                            }
                        }
                    }
                }
            }
        }
        stage('oc apply configuration') {
            steps {
                script {
                    openshift.withCluster("my-cluster") {
                        openshift.withCredentials("openshift-jenkins-external") {
                            openshift.withProject(env.OPENSHIFT_PROJECT) {
                                echo "Hello from project ${openshift.project()} in cluster ${openshift.cluster()}"
                                println openshift.apply('-f', 'config/', '-l', "app=${APP_LABEL}").out
                            }
                        }
                    }
                }
            }
        }
        stage('build application') {
            steps {
                script {
                    openshift.withCluster("my-cluster") {
                        openshift.withCredentials("openshift-jenkins-external") {
                            openshift.withProject(env.OPENSHIFT_PROJECT) {
                                echo "Hello from project ${openshift.project()} in cluster ${openshift.cluster()}"
                                def bcSelector = openshift.selector("BuildConfig", [ app : env.APP_LABEL ]) // select build
                                bcSelector.startBuild('--follow').out
                            }
                        }
                    }
                }
            }
        }




    }
}
