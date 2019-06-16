node('docker') {   
    stage 'Checkout'
        checkout scm
      
    stage 'Integration Test'
        //sh 'docker-compose -f docker-compose.integration.yml up'
        sh "ls -la"
        //sh "docker-compose -f docker-compose.yml up --force-recreate --abort-on-container-exit"
        sh "docker-compose -f docker-compose.yml up -d"
        sh "docker-compose ps"
        sh "curl http://127.0.0.1"
        sh "docker-compose -f docker-compose.yml down -v"

}
