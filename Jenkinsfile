pipeline {
    agent { label 'Docker_slave' }
    
    stages {
        stage('Checkout Git Repo') {
            steps {
                git branch: 'main',
                url: 'https://github.com/shaikharbaaz101/Hotstar-Clone.git'
            }
        }
        
        stage('Remove Old Image') {
            steps {
                sh "docker system prune --all -f"
            }
        }
        
        stage('Build New Image') {
            steps { 
                sh "docker build -t shaikhfaizan0/myhub:hotstar ."
                }
        }
        
         stage('run command docker images') {
            steps {
                sh "docker images"
            }
        }
        
        stage('Docker Credential') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'myhub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh "echo ${DOCKER_PASS} | docker login -u ${DOCKER_USER} --password-stdin"
                }
            }
        }
        
        stage('Push Image to Docker Hub') {
            steps {
                sh "docker push shaikhfaizan0/myhub:hotstar"
            }
        }


        stage('Deploy on EC2') {
            steps {
                sshagent(['ec2-ssh-key']) {
                    sh """
                        ssh -o StrictHostKeyChecking=no ubuntu@${EC2_IP} '
                        docker pull shaikhfaizan0/myhub:hotstar &&
                        docker stop hotstar-app || true &&
                        docker rm hotstar-app || true &&
                        docker run -d -p 3000:3000 --name hotstar-app shaikhfaizan0/myhub:hotstar
                        '
                    """
                }
            }
        }

    }
}
