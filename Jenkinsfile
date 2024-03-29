node {
    def app
    stage('Clone repository') {
        checkout scm
    }
    stage('Build image') {
       app = docker.build("AndrejMrceski/kiii-domasna4".toLowerCase())
    }
    stage('Push image') {   
        docker.withRegistry('https://registry.hub.docker.com', 'am-dockerhub') {
            app.push("${env.BRANCH_NAME.toLowerCase()}-${env.BUILD_NUMBER}")
            app.push("${env.BRANCH_NAME}-latest")
            // signal the orchestrator that there is a new version
        }
    }
}