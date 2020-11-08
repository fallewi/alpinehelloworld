pipeline
{
	environment
	{
	IMAGE_NAME = "fallewi/monapp"
	IMAGE_TAG = "latest"
	REGISTRY_URL = "https://index.docker.io/v2/"
	}
	agent none
	stages{
		stage ('build le conteneur'){
					agent any
					steps{
							script{			
							sh    """
									git clone  https://github.com/fallewi/alpinehelloworld.git
									cd alpinehelloworld/
									docker build -t  ${IMAGE_NAME}:${IMAGE_TAG} .
					              """
								}
						}
				}
			   
					 	stage ('lance le conteneur'){
					agent any
					steps{
							script{			
							sh    """
									docker run -d -p 80:5000 -e PORT=5000 --name hello ${IMAGE_NAME}:${IMAGE_TAG}
									sleep 5s
									docker ps
					              """
								}
						}
				}
						stage ('test d\'acceptance'){
					agent any
					steps{
							script{			
							sh    """
								curl http://localhost  | grep - q "heelo world!"
								
					              """
								}
						}
				}
					stage ('suppression du conteneur'){
					agent any
					steps{
							script{			
							sh    """
								docker stop hello
								docker rm hello
								
					              """
								}
						}
				}
		}
}
