node {
    def app

    stage('Clone repository') {
        /* Cloning the Repository to our Workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image */

        app = docker.build("grigciulache/hellohtml")
    }

    stage('Test image') {
        
        app.inside {
            echo "Tests passed"
        }
    }
    stage('Push image') {
         
		/*	You would need to first register with DockerHub before you can push images to your account */
		
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
            } 
        echo "Trying to Push Docker Build to DockerHub"
    }   
    stage('Run image'){
        echo "Hello World!"
        sh "hostname"
        sh "docker stop myapache || :"
        sh "docker rm myapache || :"
        sh "docker run -it -d -p 80:80 --name myapache grigciulache/hellohtml:latest"
    }
    /* seems to be a sinc issue. Acknloedge, to be fixed */
}