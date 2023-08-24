pipeline {
    agent any

    environment {
        APP_NAME = "gitops-demo-app"
    }
    stages{
        stage("Cleanup Workspace"){
            steps{
                script{
                    cleanWs()
                }
            }
        }
        stage("Chekout SCM"){
            steps{
                script{
                   git credentialsId: 'gitcred', 
                   url: 'https://github.com/siddharth201983/gitops-demo-config.git', 
                   branch: 'master'
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
                        sh "git push https://github.com/siddharth201983/gitops-demo-config.git master"
                    }
                }
            }
        }
    }
}