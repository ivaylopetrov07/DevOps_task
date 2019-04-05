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
                sh " docker push ivo.com:5000/django_ivaylopetrov07  "
            }
        }        
        stage('Deploy') {
            steps {
                echo 'Deploying....'
                sh "docker run -p 8000:8000 -d --name ivo ivoreg.com:5000/django_ivaylopetrov07" 
            }
        }
    }
}


