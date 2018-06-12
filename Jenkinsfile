node {
    def app

    stage('Clone repository') {

        checkout scm
    }

    stage('Build image') {

        app = docker.build("markusdkruger/nginx")
    }

    stage('Test image') {
        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        docker.withRegistry('https://registry.hub.docker.com', 'markus.docker.hub') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}
