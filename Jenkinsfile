pipeline {
    agent {label "dev-agent"}
    stages {
        stage("code clone") {
            steps {
                git url: "https://github.com/pradyuna/nodejs-cicd.git" , branch: "master"
            }
        }
        stage("build") {
            steps {
                sh "docker build . -t pradyumna810/my-nodjs-cicd-todoapp:latest"
            }
        }
        stage("docker login & push image") {
            steps {
                echo "logging into dockerhub & pushing the image"
                withCredentials([usernamePassword(credentialsId: "Dockerhub" , passwordVariable: "dockerhubpassword", usernameVariable: "dockerUser")]) {
                    sh "docker login -u ${env.dockerUser} -p ${env.dockerhubpassword}"
                    sh "docker push pradyumna810/my-nodjs-cicd-todoapp:latest"
                }
            }
        }
        stage("deploy") {
            steps {
                sh "docker run -d -p 8000:8000 pradyumna810/my-nodjs-cicd-todoapp:latest"
            }
        }
    }
}
