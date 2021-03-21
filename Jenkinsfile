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

       

        stage("pushing the images to docker hub"){
            steps{
                withDockerRegistry([ credentialsId: "48a8341e-a749-48c9-81a6-6ec073bf27db", url: "" ]){
                    bat "docker push sreelakshmi14/k8s_kanban-app:latest"
                    bat "docker push sreelakshmi14/k8s_kanban-ui:latest"
                  bat "docker push postgres:9.6-alpine"
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
