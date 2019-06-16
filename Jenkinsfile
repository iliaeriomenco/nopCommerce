node('docker') {   
    stage 'Checkout'
        checkout scm
      
    stage 'Integration Test'
        //sh 'docker-compose -f docker-compose.integration.yml up'
        sh "ls -la"
        //sh "docker-compose -f docker-compose.yml up --force-recreate --abort-on-container-exit"
        sh "docker-compose -f docker-compose.yml up -d"
        sh "docker-compose ps"
        sh "sleep 10"
        sh "ip=\$(docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' nopcommerce) && curl -I \$ip"
        sh "docker-compose -f docker-compose.yml down -v"

}
