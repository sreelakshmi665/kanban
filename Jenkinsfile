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
                bat "docker commit kanban-board_kanban-app sreelakshmi14/kanban-board_kanban-app:latest"
                bat "docker commit kanban-board_kanban-ui sreelakshmi14/kanban-board_kanban-ui:latest"
                bat "docker commit postgres sreelakshmi14/postgres:9.6-alpine"
            }
        }

        stage("pushing the images to docker hub"){
            steps{
                withDockerRegistry([ credentialsId: "83fb3bd9-d130-41d3-b0f9-3599a244c460", url: "" ]){
                    bat "docker push sreelakshmi14/kanban-board_kanban-app:latest"
                    bat "docker push sreelakshmi14/kanban-board_kanban-ui:latest"
                  bat "docker push sreelakshmi14/postgres:9.6-alpine"
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
