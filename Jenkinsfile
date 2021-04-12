properties([parameters([choice(choices:['master','develop','feature'],
description:'Select Branch to build',name:'branch')])])
node {
    def Myapp

    stage('Clone repository') {
	 echo "pulling changes from the branch ${params.branch}"
        /* Cloning the Repository to our Workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image */

        Myapp = docker.build("indu12/dockerimg-feature")
    }
    stage('Push image') {
        /* 
			You would need to first register with DockerHub before you can push images to your account
		*/
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            Myapp.push("${env.BUILD_NUMBER}")
            Myapp.push("latest")
            } 
                echo "Trying to Push Docker Build to DockerHub"
    }
}
