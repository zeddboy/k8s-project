pipeline{
    agent {
        docker{
            image 'node:14-alpine'
        }
    
    }

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
                sh "docker-compose up -d"
            }
        }

        stage("commiting the deocker images"){
            steps{
                sh "docker commit kanban-ui kunalagarwal25/challenge-ui"
                sh "docker commit kanban-app kunalagarwal25/challenge-app" 
            }
        }

        stage("pushing the images to docker hub"){
            steps{
                withDockerRegistry([ credentialsId: "dockerid", url: "" ]){
                    sh "docker push kunalagarwal25/challenge-app"
                    sh "docker push kunalagarwal25/challenge-ui"
                }
            }
        }

        stage("kubernates"){
            steps{
                sh "kubectl apply -f k8s"
            }
        }
    }
}
