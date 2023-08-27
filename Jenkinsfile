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
        stage("docker login") {
            steps {
                echo "============= docker login ========================="
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-dyonisii') {
                    }
                }
            }
        }
        stage("create docker image") {
            steps {
                echo " ============== start building image ================"
                dir ('.') {
                	sh 'docker build -t dyonisii/webapp:$BUILD_ID . '      //BUOLD_ID
                    sh 'ls -la'
               }
            }
        }
 //       stage('docker run') {
 //           steps {
   //             echo "=============== docker run =================="
       //        script {
         //           def tomcatContainer = docker.image('dyonisii/webapp:$BUILD_ID')
         //           def container = tomcatContainer.run("-p 7777:80")
         //           try {
          //              //sleep(time: 15, unit: 'SECONDS')
           //         } finally {
       ////                 sh "sleep 20"
         //               sh 'ls -la'
         //               sh "docker stop ${container.id}"
            //            sh "docker rm ${container.id}"
         //           }
         //       }
       //     }
     //   }
         stage("docker push") {
            steps {
                echo " ============== start pushing image =================="               
                sh '''
                docker push dyonisii/webapp:$BUILD_ID
                ls -la
                '''
                //sh "docker rmi ${container.id}"
            }
        }
    }
}
