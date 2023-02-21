pipeline{
    agent any
    stages{
        stage(code){
            steps{
                echo 'Pulling code from GITHUB'
                git url: 'https://github.com/PiyushPatil9111/django-todo-app.git', branch: 'develop'
            }
        }
        stage(test){
            steps{
                echo 'Testing code pulled from GITHUB'
            }
        }
        stage(build){
            steps{
                echo 'Building the code from tested stage'
                sh 'docker build . -t awsstudy911/todo-app:latest'
            }
        }
        stage(push){
            steps{
                echo 'Pushing the code from built stage'
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
                 sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                 sh "docker push awsstudy911/todo-app:latest"
            }
        }
        }
        stage(deploy){
            steps{
                sh "sudo docker-compose -p 'mycont' down --rmi all && sudo docker-compose up -d --build"
            }
        }
    }
}
    
