pipeline {
    agent any

    stages {
        stage ("Build Docker Image and Tag") {
            steps {
                sh "docker build --tag crypto:latest ."
                sh "docker tag crypto:latest 19127392/19127392::latest"
            }
        }
        stage ("Publish to Docker Hub") {
            steps {
                withDockerRegistry(credentialsId: "dockerhub", url: "") {
                    sh "docker push 19127392/19127392:latest"
                }
            }
        }
        stage ("Deploy app to container") {
            steps {
                sh "docker pull 19127392/19127392::latest"
                sh "docker rm -f web-server || true"
                sh "docker run --name web-server --rm -dp 3000:3000 crypto:latest"
            }
        }
    }
}
