pipeline {
    agent { label 'Ubuntu_ansible' }
    stages {
        stage("Checkout") {
            steps {
                echo "============= Cloning repository =================="
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']], 
                    userRemoteConfigs: [[url: 'https://github.com/Dyonisii/App-for-jenkins.git']] 
                ])
            }
        }
        stage('docker run') {
            steps {
                echo "============= docker run =================="
                script {
                    def imageName = 'dyonisii/k8stest:latest'
                    def containerName = imageName.replaceAll('/', '_').replaceAll(':', '_')
                    
                    // Остановить существующий контейнер с указанным именем, если он запущен
                    try {
                        sh "docker stop $containerName"
                        sh "docker rm $containerName"
                    } catch (Exception e) {
                        // Пропустить ошибку, если контейнер не был найден или не запущен
                    }
                    
                    def tomcatContainer = docker.image(imageName)
                    def container = tomcatContainer.run("-p 7777:80", name: containerName)
                    try {
                        // Ваш код здесь
                    } finally {
                        sh "sleep 20"
                        sh "docker stop ${container.id}"
                    }
                }
            }
        }
    }
}
