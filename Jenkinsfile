/* repo reside in Jenkins job, checkout scm does checkout with selected branch,
tag variable is defined in Jenkins job, as build with paramaters
*/
node {
    def app

    // Step 1
    stage('Clone repository') {
        checkout scm   
    }

    // Step 2
    stage('Build image') {
        loginDocker()
        buildImage()
    }
   
    // Step 3
    stage('Push image') {
        sh "sudo docker push satoshegen/php-trivago:${tag}"
        sh "sudo docker rmi satoshegen/php-trivago:${tag}"
    }
    // Step 4
    stage('Rollout deployment') {
        sh "kubectl set image deployment webserver php-apache=satoshegen/php-trivago:${tag}"
        sh "kubectl rolling-update webserver -f webserver.yaml"
    }

    stage('Clean working directory') {
        deleteDir()
    }
}


// Functions
def buildImage(){
    sh "sudo docker build --no-cache -t satoshegen/php-trivago:${tag} ."
}

def loginDocker(){
   sh "docker login --username=${DOCKER_USER} --password=${DOCKER_PASS}"
        }
    



