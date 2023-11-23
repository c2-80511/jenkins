pipeline {
    agent any

    stages {
        stage ('SCM') {
            steps {
                git branch: 'master', url: 'https://github.com/c2-80511/jenkins.git'
            }
        }
        
        stage ('docker login') {
            steps {
                sh 'echo <token> | /usr/bin/docker login -u prasadthombare --password-stdin'
            }
        }
        stage ('docker build image') {
            steps {
                sh '/usr/bin/docker image build -t prasadthombare/mywebsite .'
            }
        }
        
          stage ('docker push image') {
            steps {
                sh '/usr/bin/docker image push prasadthombare/mywebsite'
            }
        }
        
         stage ('docker remove service') {
            steps {
                sh '/usr/bin/docker service rm myserivce'
            }
        }
        stage ('docker create service') {
            steps {
                sh '/usr/bin/docker service create --name myserivce -p 9090:80 --replicas 5 prasadthombare/mywebsite'
            }
        }
    }
}
