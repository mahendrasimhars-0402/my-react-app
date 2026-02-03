pipeline{
agent any

environment{
	IMAGE_NAME:'mahendrasimha0403/my-react-app'
}

stages{
stage('Checkout code')
{
steps
{
	git branch:'main',
	url:'git@github.com:mahendrasimhars-0402/my-react-app.git'
}
}
stage('Install Dependencies')
{
steps
{
	sh 'npm install'
}
}
stage('Build docker Image')
{
steps
{
scripts
{
	dockerImage=docker.build("${IMAGE_NAME}:latest")
}
}
}
stage('Push Image to DockerHub')
{
steps
{
scripts
{
	docker.withRegistry('http://index.docker.io/v1/', dockerhub){
	dockerImage.push()
}
}
}
}
}
post
{
success{
	echo "Pipeline build successfully!"
}
failure{
	echo "Pipeline build Failed!!!!"
}
}
}

