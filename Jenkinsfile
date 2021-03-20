pipeline{
    agent any

    stages{
        stage("docker build"){
            steps{
                bat "docker-compose up"
            }
        }
        stage("uploading to docker hub"){
            steps{
                bat "docker commit kaban-ui bharathvelisala/challenge-ui"
                bat "docker push bharathvelisala/challenge-ui"
                bat "docker commit kaban-app bharathvelisala/challenge-app"
                bat "docker push bharathvelisala/challenge-app"
            }
        }

        stage("kubernates"){
            steps{
                bat "kubectl apply -f k8s"
            }
        }
    }
}