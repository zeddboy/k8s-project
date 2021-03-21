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

        stage("commiting the deocker images"){
            steps{
                bat "docker commit kanban-ui kunalagarwal25/challenge-ui"
                bat "docker commit kanban-app kunalagarwal25/challenge-app" 
            }
        }

        stage("pushing the images to docker hub"){
            steps{
                withDockerRegistry([ credentialsId: "dockerid", url: "" ]){
                    bat "docker push kunalagarwal25/challenge-app"
                    bat "docker push kunalagarwal25/challenge-ui"
                }
            }
        }

        stage("kubernates"){
            steps{
                bat "kubectl apply -f k8s"
            }
        }
    }
}
