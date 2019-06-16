node('docker') {   
    stage 'Checkout'
        checkout scm
    
    try {
    stage 'Integration Test'
        //sh "docker-compose -f docker-compose.yml up --force-recreate --abort-on-container-exit"
        sh "docker-compose -f docker-compose.yml up -d"
        sh "docker-compose ps"
        //sh "ip=\$(docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' nopcommerce) && curl -v \$ip"
        //sh "curl http://127.0.0.1"
        sh "docker-compose -f docker-compose.yml down -v"
    }
    
    catch (e) {
    // If there was an exception thrown, the build failed
    currentBuild.result = "FAILED"
        throw e}
    
    finally {
    stage 'Slack Notification'
        slackSend channel: 'tt_builds', 
        color: 'good', 
        //message: 'started ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)', 
        message: """FINISHED: "Job: ${env.JOB_NAME}, Build: [${env.BUILD_NUMBER}], Result: ${currentBuild.currentResult}" (<${env.BUILD_URL}|Open>)""",
        teamDomain: 'glossasystems', 
        tokenCredentialId: 'jenkins-slack-integration'
    }
}
