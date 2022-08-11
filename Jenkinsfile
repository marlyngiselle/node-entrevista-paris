pipeline {
    agent { label 'nodejs' }

    stages {


        stage('Build') {
            steps {
                // sh 'docker stop contenedor' || echo "No hay contenedor corriendo"
                // sh 'docker rm contenedor' || echo "No hay contenedor para borrar"
                sh 'docker build -t mgiselle/${JOB_NAME}:v${BUILD_NUMBER} .'
            }
        }

        stage('Test') {
            steps {
                echo 'Ingresa en la pagina y prueba tu mismo'
            }
        }

        stage('Release') {
            steps {
                sh 'docker tag mgiselle/${JOB_NAME}:v${BUILD_NUMBER} mgiselle/${JOB_NAME}:latest'
                sh 'docker login -u="mgiselle" -p="Tasia.2411"'
                sh 'docker push mgiselle/${JOB_NAME}:v${BUILD_NUMBER}'
                sh 'docker push mgiselle/${JOB_NAME}:latest'
                sh 'docker rmi mgiselle/${JOB_NAME}:v${BUILD_NUMBER}'
                sh 'docker rmi mgiselle/${JOB_NAME}:latest'
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker run -d -p 80:3000 --name appnodejs mgiselle/${JOB_NAME}:latest'
            }
        }

    }
}