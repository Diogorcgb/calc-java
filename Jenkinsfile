pipeline
{
	agent any

	parameters
	{
		string(name: 'DOCKER_IMAGE', defaultValue: 'default_name', description: 'Docker image')
		string(name: 'DOCKER_CONTAINER', defaultValue: 'default_name', description: 'Docker container')
		string(name: 'PORT', defaultValue: '3000', description: 'Port')
	}

    stages
    {

  
        stage('Docker build'){
            steps
            {
				sh "docker rmi -f ${DOCKER_IMAGE}"
				sh "docker build -t ${DOCKER_IMAGE} ."
                sh "docker login -u admin -p Drcg#1470 localhost:8082 "
				sh "docker tag ${DOCKER_IMAGE} localhost:8082/${DOCKER_IMAGE}:latest}"
				sh "docker push localhost:8082/${DOCKER_IMAGE}:latest"
                sh "javac *.java"
                sh "jar cfe calculator.jar Calculadora2 ./*.class"
                sh "curl -v --user 'admin:Drcg#1470' --upload calculator.jar"

            }
        }
		

		

    }
}