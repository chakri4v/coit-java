pipeline{
    agent any
        stages{
            stage('Build'){
                steps{
                    // sh 'cd coit-backend1'
                    sh 'docker build -t chakri4/coit-backend1:1.0.0 -f Docker-multistagefile .'
                    sh 'docker run -d -p 8080:8080 --name coit chakri4/coit-backend1:1.0.0'
                    sh 'sleep 2'
                    sh "container=`docker ps | grep coit | awk '{print \$1}'`"
                    sh "docker stop $container"
                    sh "stopped=`docker ps -a| grep coit | awk '{print \$1}'`"
                    sh "docker rm $stopped"
                    sh "image=`docker images | grep coit | awk '{print \$3}'`"
                    sh "docker rmi $image"

                // providing docker credentials
                
                    withCredentials([
                        usernamePassword(credentials:'DockerHub' , usernameVariable: USER, passwordVariable: PASS)
                    ])
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh "docker push chakri4/coit-backend1:1.0.0"
                }                
            }
        
    }    
}
