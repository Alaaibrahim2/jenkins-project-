pipeline{
    agent any
    
    stages{
        stage('build'){
            steps{
                script{
                    git branch: 'deployment', url: 'https://github.com/Alaaibrahim2/jenkins-project-.git'
                    sh 'docker build -t java-app .'
                }
            }
        }

        stage('push'){
            steps{
                script{
                    withCredentials([usernamePassword(credentialsId: 'docker-hub', passwordVariable: 'Password', usernameVariable: 'Username')]) {
                    sh 'docker login --username $Username --password $Password'
                    sh 'docker tag java-app $Username/java-app'
                    sh 'docker push $Username/java-app'
                    }
                }
            }
        }

        stage('deploy'){
            steps{
                script{
                    withAWS(credentials: 'aws-cli', region: 'eu-north-1') {
                    sh 'aws eks update-kubeconfig --region eu-north-1 --name my-eks-cluster'
                    sh 'kubectl apply -f ./k8s/deployment.yaml'
                    }
                }
            }
        }
    }
}
