pipeline{
    agent any
    
    stages{
        stage('code'){
            steps{
                echo "cloning .... .."
                git url: 'https://github.com/surajc5/node-todo-cicd.git',branch: 'master'
            }
        }
        stage('Build'){
            steps{
                echo "Build .... .."
                sh 'docker build . -t node-todo-app'
            }
        }
         stage('push to Docker Hub'){
            steps{
                echo "pushing  to the Docker Hub ......"
                withCredentials([usernamePassword(credentialsId: "dockerHub",usernameVariable: "USERNAME", passwordVariable: "PASS")]){
                sh "docker tag node-todo-app ${env.USERNAME}/node-todo-app:latest"
                sh "docker login -u ${env.USERNAME} -p ${env.PASS}"
                sh "docker push ${env.USERNAME}/node-todo-app:latest"
                }
                
                
            }
        }
        stage('Deploy'){
            steps{
                echo "Deploying .... .."
                sh "docker-compose down && docker-compose up -d"
                
            }
        }
    }
}
