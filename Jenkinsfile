pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh " docker build -t django_ivaylopetrov07:latest ." 
            }
        }
       stage('Tag') {
            steps {
                echo 'Taggging..'
                sh " docker login -u test -p password ivoreg.com:5000/django_ivaylopetrov07"
                sh " docker tag django_ivaylopetrov07:latest ivoreg.com:5000/django_ivaylopetrov07"
            }
        }
        stage('Push') {
            steps {
                echo 'Pushing to the local registry..'
                sh " docker push ivoreg.com:5000/django_ivaylopetrov07  "
            }
        }        
        stage('Deploy') {
            steps {
                echo 'Deploying....'
                sh "docker -h ansible@192.168.162.11 run -p 8000:8000 -d --name ivo3 ivoreg.com:5000/django_ivaylopetrov07" 
            }
        }
    }
}


