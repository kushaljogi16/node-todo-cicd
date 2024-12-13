pipeline {
    agent any
    stages {
        stage("code"){
            steps{
                git url: "https://github.com/kushaljogi16/node-todo-cicd.git", branch: "master"
                echo "Clone the repo"
            }
        }
        stage("build image"){
            steps{
                sh "docker build -t kushaljogi16/mysampletestimage ."
                echo "Docker image is build"
            }
        }
        stage("push image"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerhubPass",usernameVariable:"dockerhubUser")]){
                sh "docker login -u ${env.dockerhubUser} -p ${env.dockerhubPass}"
                sh "docker tag kushaljogi16/mysampletestimage:latest kushaljogi16/mysampletestimage:latest"
                sh "docker push kushaljogi16/mysampletestimage:latest"
                echo 'pushed docker image to dockerhub' 
                }
            }          
            }
        stage("deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
                echo 'Deployed container using image'  
            }
        }
    }
}


// pipeline {
//     agent any
    
//     stages {
        
//         stage("code"){
//             steps{
//                 git url: "https://github.com/kushaljogi16/node-todo-cicd.git", branch: "master"
//                 echo 'bhaiyya code clone ho gaya'
//             }
//         }
//         stage("build and test"){
//             steps{
//                 sh "docker build -t kushaljogi16/mydemoimage:latest ."
//                 echo 'code build bhi ho gaya'
//             }
//         }
//         stage("scan image"){
//             steps{
//                 echo 'image scanning ho gayi'
//             }
//         }
//         stage("push"){
//             steps{
//                 withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerhubPass",usernameVariable:"dockerhubUser")]){
//                 sh "docker login -u ${env.dockerhubUser} -p ${env.dockerhubPass}"
//                 sh "docker tag kushaljogi16/mydemoimage:latest kushaljogi16/mydemoimage:latest"
//                 sh "docker push kushaljogi16/mydemoimage:latest"
//                 echo 'image push ho gaya'
//                 }
//             }
//         }
//         stage("deploy"){
//             steps{
//                 sh "docker-compose down && docker-compose up -d"
//                 echo 'deployment ho gayi'
//             }
//         }
//     }
// }
    
