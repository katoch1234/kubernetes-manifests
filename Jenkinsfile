pipeline {
    agent {
        label 'jenkins-agent'
    }

    environment {
        REPO_URL = 'https://github.com/katoch1234/kubernetes-manifests.git'
        BRANCH = 'main'
        GIT_CREDENTIALS = 'your-jenkins-credentials-id'  // Replace with your Jenkins credentials ID
        GIT_USER_NAME = 'Vaibhav Katoch'
        GIT_USER_EMAIL = 'katochvaibhav3@gmail.com'
    }

    stages {
        sstage('git checkout') {
            steps{
                git branch: 'main', credentialsId: 'github', url:'https://github.com/katoch1234/kubernetes-manifests.git'
            }
        }}

        stage('Update Image in deployment.yaml') {
            steps {
                script {
                    sh "git config user.email '${GIT_USER_EMAIL}'"
                    sh "git config user.name '${GIT_USER_NAME}'"
                    sh "sed -i 's|595496445232\\.dkr\\.ecr\\.us-east-1\\.amazonaws\\.com\\/vaibhav.*|595496445232\\.dkr\\.ecr\\.us-east-1\\.amazonaws\\.com\\/vaibhav:${DOCKERTAG}|g' deployment.yaml"
                    sh "cat deployment.yaml"
                    sh "git add deployment.yaml"
                    sh "git commit -m 'Updated image in deployment.yaml by Jenkins Job: ${env.BUILD_NUMBER}'"
                    sh "git push origin ${BRANCH}"
                }
            }
        }
    }
}