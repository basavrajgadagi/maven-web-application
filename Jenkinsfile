pipeline{

    agent any

    tools
    {
        maven 'Maven_3.9.7'
    }

    environment
    {
        buildNumber = "${BUILD_NUMBER}"
    }

    stages
    {
        stage('Git Checkout')
        {
            steps()
            {
                git branch: 'docker_cicd', url:'https://github.com/basavrajgadagi/maven-web-application.git'
            }
        }

        stage('Build Project Artifact using Maven')
        {
            steps()
            {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image')
        {
            steps()
            {
                sh 'docker build -t mithuntechnologies/dockercicd:${buildNumber} .'
            }
        }

        stage('Push Docker Image to Docker Hub Registry')
        {
            steps(
                {
                    withCredentials([string(credentialsId: 'Docker_Hub_Password', variable: 'Docker_Hub_Password')])
                    {
                            sh 'docker login -u mithuntechnologies -p ${Docker_Hub_Password}'
                    }
                    sh 'docker push mithuntechnologies/dockercicd:${buildNumber}'
                }
            )
        }
    }
}
