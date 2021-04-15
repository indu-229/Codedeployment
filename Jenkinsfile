properties([parameters([[$class: 'ChoiceParameter', choiceType: 'PT_SINGLE_SELECT', description: 'Select a branch to build', filterLength: 1, filterable: false, name: 'Branch', randomName: 'choice-parameter-87163950444300', script: [$class: 'GroovyScript', fallbackScript: [classpath: [], sandbox: false, script: ''], script: [classpath: [], sandbox: false, script: 'return[\'master\',\'develop\',\'feature\',\'feature-1\']']]]])])
node{
    def Myapp

    stage('Clone repository') {
	 echo "pulling changes from the branch ${params.branch}"
        /* Cloning the Repository to our Workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image */

        Myapp = docker.build("indu12/dockerimage-master")
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
