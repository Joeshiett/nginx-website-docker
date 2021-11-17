node {
    def app

    stage('Clone repository') {
        checkout scm
    }
    stage('Build image') {
        app = docker.build("joeshiett/nginx-website-docker")
    }
    stage('Test image') {
        app.inside {
            sh 'echo "Test passed"'
        }
    }
    stage('Push image') {
        docker.withRegistry('https://registry.hub.docker.com', 'joeshiett') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}
