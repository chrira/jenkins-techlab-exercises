properties([
    parameters([
        string(name: 'COMPANY_PARAMETER', defaultValue: 'puzzle', description: 'The company the pipeline runs in')
    ])
])

node {
    stage('Build') {
        echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL} in company ${params.company_parameter}"
    }
}
