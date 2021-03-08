pipeline
{
	agent any

	parameters
	{
		string(name: 'DOCKER_IMAGE', defaultValue: 'default_name', description: 'Docker image')

	}

    stages
    {

  
        stage('Docker build'){
            steps
            {
				sh "docker rmi -f ${DOCKER_IMAGE}"
				sh "docker build -t ${DOCKER_IMAGE} ."
	        sh "docker login -u admin -p Drcg#1470 localhost:8082 "
		sh "docker tag ${DOCKER_IMAGE} localhost:8082/${DOCKER_IMAGE}"
		sh "docker push localhost:8082/${DOCKER_IMAGE}"
                sh "javac *.java"
                sh "jar cfe calculator.jar Calculadora2 ./*.class"
                sh "curl -v -u 'admin:Drcg#1470' --upload calculator.jar http://nexus:8081/repository/java-calc/"

            }
        }
        stage('SonarQube analysis') {
       environment { scannerHome = tool 'sonarqube' }
                    steps {
                            withSonarQubeEnv('sonarqube') {
                                    sh "${scannerHome}/bin/sonar-scanner \
                                    -D sonar.login=65aa459a2fdc71b3d8ee2e5ffc715db2acf51033 \
                                    -D sonar.projectKey=sonarqube \
                                    -D sonar.java.binaries=/var/jenkins_home/workspace/Desnvolvimento \
                                    -D sonar.java.source=11 \
                                    -D sonar.host.url=http://sonarqube:9000/"
                            }
                        }
                    } 
		

        }

    }
}
