 pipeline {
    agent { label 'Ubuntu_AWS' }
    stages {
        stage("docker login") {
            steps {
                echo "============= docker login =================="
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-dyonisii') {
                        //sh 'docker pull your-image:tag'
                       // sh 'docker run -d your-image:tag'
                    }
                }
            }
        }
        stage('docker run') {
            steps {
                echo "============= docker run =================="
                script {
                    def tomcatContainer = docker.image('k8stest')
                    def container = tomcatContainer.run("-p 7777:80")
                    
                    try {
                        //sleep(time: 15, unit: 'SECONDS')
                         
                    } finally {
                    
                        sh "sleep 20"
                        sh "docker stop ${container.id}"
                        sh "docker rm ${container.id}"
                    }
                }
            }
        }
    }
}
