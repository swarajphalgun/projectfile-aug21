
node {
	def application = "apache-custom"
	def dockerhubaccountid = "tadpiku2019"
	stage('Clone repository') {
		checkout scm
	}

	stage('Build image') {
		app = docker.build("${dockerhubaccountid}/${application}:${BUILD_NUMBER}")
	}

	stage('Push image') {
		withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
		app.push()
		app.push("latest")
	}
	} 

	stage('Deploy') {
		sh ("docker run -tid -p 5000:80 -v /home/swarajphalgungm/demo/:/var/www/html/ ${dockerhubaccountid}/${application}:${BUILD_NUMBER}")
	}
	
	stage('Remove old images') {
		// remove docker old images
		sh("docker rmi ${dockerhubaccountid}/${application}:latest -f")
   }
} 
