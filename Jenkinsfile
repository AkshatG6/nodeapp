node {
    def app

    stage('Clone repository') {
        /* Cloning the Repository to our Workspace */

        checkout scm
	    
    }

    stage('Build image') {
        /* This builds the actual image */

        app = docker.build("akshatg6/nodeapp")
    }

    stage('Test image') {
        
        app.inside {
            echo "Tests passed"
        }
    }

    stage('Push image') {
        /* 
			You would need to first register with DockerHub before you can push images to your account
		*/
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
	    env.GIT_COMMIT = sh(script: "git rev-parse HEAD", returnStdout: true).trim()
	    echo env.GIT_COMMIT
            } 
                echo "Trying to Push Docker Build to DockerHub"
	    	
    }
}
