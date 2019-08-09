pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                echo 'Checkout-ing project'
                git 'https://github.com/Grisilda/apiGW.git'
                echo 'Checkout Success!'
            }
        }
        stage('Build Artifact') {
            steps {
                echo 'Building artifact...'
                sh 'mvn clean install'
                echo 'Success'
            }
        }
        stage('Create artifact copy') {
            steps {
                sh 'cp target/apigateway-*.jar target/apigateway.jar'
            }
        }
        
        stage('Create Docker Image') {
            steps {
                sh 'docker build -t demo_image .'
            }
        }
        stage('Run Container') {
            steps {              
                sh 'docker run -d -p 8084:8080 --name demoServer demo_image'           
            }
        }
    }
}
