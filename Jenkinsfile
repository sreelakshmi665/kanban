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
                bat "docker commit kanban-app sreelakshmi14/dockerrepo:app"
                bat "docker commit kanban-ui sreelakshmi14/dockerrepo:ui" 
            }
        }

       

        stage("pushing the images to docker hub"){
            steps{
                withDockerRegistry([ credentialsId: "48a8341e-a749-48c9-81a6-6ec073bf27db", url: "https://registry.hub.docker.com" ]){
                    bat "docker tag dockerrepo:app sreelakshmi14/dockerrepo:app"
                    bat "docker push sreelakshmi14/dockerrepo:app"
                    bat "docker push sreelakshmi14/dockerrepo:ui"
                  
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
