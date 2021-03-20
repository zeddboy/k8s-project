pipeline{
    agent any

    stages{

        // stage("removing docker images if exists"){
        //     steps{
        //         bat "docker rm kanban-postgres"
        //         bat "docker rm kanban-app"
        //         bat "docker rm kanban-ui"
        //     }
        // }
        stage("docker build"){
            steps{
                bat "docker-compose up -d"
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