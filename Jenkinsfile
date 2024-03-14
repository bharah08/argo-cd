pipeline {
    agent any

environment {
    GIT_REPO_NAME = "argo-cd"
    GIT_USER_NAME = "bharah08"
    NEW_IMAGE_NAME = "bharath0812/bank:1.0"
    
}


    stages {
        stage('checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/bharah08/argo-cd.git'
            }
        }
        
        stage('deploy with argocd'){
           steps {
                script {
                    withCredentials([string(credentialsId: 'github-tokken', variable: 'GITHUB_TOKEN')]) {
                       sh "sed -i 's|image: .*|image: $NEW_IMAGE_NAME|' deployment.yml"
                       sh 'git add deployment.yml'
                       sh "git commit -m 'Update deployment image to $NEW_IMAGE_NAME'"
                       sh "git push https://${GITHUB_TOKEN}@github.com/${GIT_USER_NAME}/${GIT_REPO_NAME} HEAD:main"
                    }
                }
            }
        }
    }
}
