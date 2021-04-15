properties([parameters([[$class: 'ChoiceParameter', choiceType: 'PT_SINGLE_SELECT', description: '', filterLength: 1, filterable: false, name: '', randomName: 'choice-parameter-93618894495400', script: [$class: 'GroovyScript', fallbackScript: [classpath: [], sandbox: false, script: ''], script: [classpath: [], sandbox: false, script: '''def gettags = ("git ls-remote -t -h ssh://jenkins@<mygitpath>/repo/some.git feature/*").execute()
return gettags.text.readLines().collect{
it.split()[1].replaceAll(\'refs/heads/\',\'\').replaceAll(\'refs/tags/\',").replaceAll("\\\\^\\\\{\\\\}",")
}''']]]])])
node
{
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
