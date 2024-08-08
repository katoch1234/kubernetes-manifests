pipeline {
    agent{
        label 'jenkins-agent'
    }
}

stages{
        stage('git checkout') {
            checkout scm
        }

        stage('update image in deployment.yaml')
        {
            steps {
                script{
                    sh "git config user.email katochvaibhav3@gmail.com"
                        sh "git config user.name vaibhav "
                        //sh "git switch master"
                        sh "cat deployment.yaml"
                        sh "sed -i 's/595496445232\.dkr\.ecr\.us-east-1\.amazonaws\.com\/vaibhav:${BUILD_NUMBER}/595496445232\.dkr\.ecr\.us-east-1\.amazonaws\.com\/vaibhav:${DOCKERTAG}/g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push HEAD:main"
                    
                }
            }
        }