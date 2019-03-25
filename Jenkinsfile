pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                    def remote = [:]
                    remote.name = 'root'
                    remote.host = '192.168.162.3'
                    remote.user = 'root'
                    #remote.password = 'password'
                    remote.allowAnyHosts = true
                           stage('Remote SSH') {
                            sshCommand remote: remote, command: "docker build -t django_ivaylopetrov07:latest ."
                               sshCommand remote: remote, command: "for i in {1..5}; do echo -n \"Loop \$i \"; date ; sleep 1; done"
    } 
            }
        }
       stage('Tag') {
            steps {
                echo 'Taggging..'
                sh " docker login -u test -p password registrydomain.com:5000/django_ivaylopetrov07"
                sh " docker tag django_ivaylopetrov07:latest registrydomain.com:5000/django_ivaylopetrov07"
            }
        }
        stage('Push') {
            steps {
                echo 'Pushing to the local registry..'
                sh " docker push registrydomain.com:5000/django_ivaylopetrov07  "
            }
        }        
        stage('Deploy') {
            steps {
                echo 'Deploying....'
                sh "docker run -p 8000:8000 -d registrydomain.com:5000/django_ivaylopetrov07" 
            }
        }
    }
}
