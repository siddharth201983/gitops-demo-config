pipeline {
    agent any
<<<<<<< HEAD

    environment {
        DOCKERHUB_USERNAME = "siddharth20"
        APP_NAME = "gitops-demo-app"
        IMAGE_TAG = "${BUILD_NUMBER}"
        IMAGE_NAME = "${DOCKERHUB_USERNAME}/${APP_NAME}"
        REGISTRY_CREDS = 'dockerhub'
    }
    stages{
        stage("Cleanup Workspace"){
            steps{
                script{
=======
    environment {
        DOCKERHUB_USERNAME = "kunchalavikram"
        APP_NAME = "gitops-demo-app"
        IMAGE_TAG = "${BUILD_NUMBER}"
        IMAGE_NAME = "${DOCKERHUB_USERNAME}" + "/" + "${APP_NAME}"
        REGISTRY_CREDS = 'dockerhub'
        }
    stages {
        stage('Cleanup Workspace'){
            steps {
                script {
>>>>>>> main
                    cleanWs()
                }
            }
        }
<<<<<<< HEAD
        stage("Chekout SCM"){
            steps{
                script{
                   git credentialsId: 'gitcred', 
                   url: 'https://github.com/siddharth201983/gitops-demo.git', 
                   branch: 'master'
                }
            }
        }
        stage("Build Docker Image"){
            steps{
                script{
                   docker_image = docker.build "${IMAGE_NAME}"
                }
            }
        }
        stage("Push Image to Docker"){
            steps{
                script{
                   docker.withRegistry('', REGISTRY_CREDS){
                        docker_image.push("${BUILD_NUMBER}")
                        docker_image.push("latest")
                   }
                }
            }
        }
        stage("Delete Docker Images"){
            steps{
                script{
                    sh "docker rmi ${IMAGE_NAME}:${IMAGE_TAG}"
                    sh "docker rmi ${IMAGE_NAME}:latest"
                }
            }
        }
        stage("Update K8s deployment yaml"){
            steps{
                script{
                    sh "cat deployment.yml"
                    sh "sed -i 's/${APP_NAME}.*/${APP_NAME}:${IMAGE_TAG}/g' deployment.yml"
                    sh "cat deployment.yml"
                }
            }
        }
        stage("Push the changed deployment file to git"){
            steps{
                script{
                    sh """
                        git config --global user.name "siddharth201983"
                        git config --global user.email "sharma.siddharth2009@gmail.com"
                        git add deployment.yml
                        git commit -m "updated the deployment file"
                    """
                    withCredentials([gitUsernamePassword(credentialsId: 'gitcred', gitToolName: 'Default')]) {
                        sh "git push https://github.com/siddharth201983/gitops-demo-config.git master --allow-unrelated-histories"
=======
        stage('Checkout SCM'){
            steps {
                git credentialsId: 'github', 
                url: 'https://github.com/kunchalavikram1427/gitops-demo.git',
                branch: 'dev'
            }
        }
        stage('Build Docker Image'){
            steps {
                script{
                    docker_image = docker.build "${IMAGE_NAME}"
                }
            }
        }
        stage('Push Docker Image'){
            steps {
                script{
                    docker.withRegistry('', REGISTRY_CREDS ){
                        docker_image.push("${BUILD_NUMBER}")
                        docker_image.push('latest')
                    }
                }
            }
        } 
        stage('Delete Docker Images'){
            steps {
                sh "docker rmi ${IMAGE_NAME}:${IMAGE_TAG}"
                sh "docker rmi ${IMAGE_NAME}:latest"
            }
        }
        stage('Updating Kubernetes deployment file'){
            steps {
                sh "cat deployment.yml"
                sh "sed -i 's/${APP_NAME}.*/${APP_NAME}:${IMAGE_TAG}/g' deployment.yml"
                sh "cat deployment.yml"
            }
        }
        stage('Push the changed deployment file to Git'){
            steps {
                script{
                    sh """
                    git config --global user.name "vikram"
                    git config --global user.email "vikram@gmail.com"
                    git add deployment.yml
                    git commit -m 'Updated the deployment file' """
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'pass', usernameVariable: 'user')]) {
                        sh "git push http://$user:$pass@github.com/kunchalavikram1427/gitops-demo.git dev"
>>>>>>> main
                    }
                }
            }
        }
    }
}

<<<<<<< HEAD
=======

// stage('Build Docker Image'){
//             steps {
//                 sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
//                 sh "docker build -t ${IMAGE_NAME}:latest ."
//             }
//         }
//         stage('Push Docker Image'){
//             steps {
//                 withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'pass', usernameVariable: 'user')]) {
//                     sh "docker login -u $user --password $pass"
//                     sh "docker push ${IMAGE_NAME}:${IMAGE_TAG} ."
//                     sh "docker push ${IMAGE_NAME}:latest ."
//                 }
//             }
//         }
>>>>>>> main
