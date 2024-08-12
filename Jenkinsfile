pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/katoch1234/kubernetes-manifests.git'
        BRANCH = 'main'
        GIT_CREDENTIALS = 'github-creds'  // Replace with your Jenkins credentials ID
        GIT_USER_NAME = 'cu.16bcs1092'
        GIT_USER_EMAIL = 'cu.16bcs1092@gmail.com '
    }

    stages {
        
        stage('Update Image in deployment.yaml') {
            steps {
                script {
                    withCredentials([gitUsernamePassword(credentialsId: 'github-creds', gitToolName: 'git-tool')]) {
                   /* sh "git clone https://github.com/katoch1234/kubernetes-manifests.git"
                    sh "git config --global user.email '${GIT_USER_EMAIL}'"
                    sh "git config --global user.name '${GIT_USER_NAME}'" */
                    sh "sed -i 's|595496445232\\.dkr\\.ecr\\.us-east-1\\.amazonaws\\.com\\/vaibhav.*|595496445232\\.dkr\\.ecr\\.us-east-1\\.amazonaws\\.com\\/vaibhav:${DOCKERTAG}|g' deployment.yaml"
                    sh "cat deployment.yaml"
                    sh "pwd && ls -lhtra" 
                    sh "git add ."
                    sh "git commit -m 'Updated image in deployment.yaml by Jenkins Job: ${env.BUILD_NUMBER}'"
                    sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kubernetes-manifests.git HEAD:main"
                }
                }
            }
        }
    }
}
