pipeline {
    agent any

    stages {
        stage('Checkout i211215') {
            steps {
                git 'https://github.com/M-Abdullah03/simple-reactjs-app.git'
            }
        }

        stage('Install Dependencies i211215') {
            steps {
                bat 'npm install'
            }
        }
        stage('Build Docker Images i211215') {
            steps {
                script {
                    def appNames = ['Auth', 'Classrooms', 'client', 'event-bus', 'Post']
                    def imageNames = ['auth', 'class', 'client', 'event-bus', 'post']
                    for (let i = 0; i < appNames.length; i++) {
                        def appName = appNames[i]
                        def imageName = imageNames[i]
                        withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                            bat "docker build -t %DOCKER_USERNAME%/final/${imageName} ./${appName}"
                        }
                    }
                }
            }
        }
        stage('Run Docker Image i211215') {
            steps {
                script {
                    def appNames = ['Auth', 'Classrooms', 'client', 'event-bus', 'Post']
                    def imageNames = ['auth', 'class', 'client', 'event-bus', 'post']
                    for (let i = 0; i < appNames.length; i++) {
                        def appName = imageNames[i]
                        withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                            bat "docker run -d %DOCKER_USERNAME%/final/${appName}"
                        }
                    }
                }
            }
        }

        stage('Push Docker Image i211215') {
            steps {
                script {
                    def appNames = ['Auth', 'Classrooms', 'client', 'event-bus', 'Post']
                    def imageNames = ['auth', 'class', 'client', 'event-bus', 'post']
                    for (let i = 0; i < appNames.length; i++) {
                        def appName = imageNames[i]
                        withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                            bat 'docker login -u %DOCKER_USERNAME% -p %DOCKER_PASSWORD%'
                            bat "docker push %DOCKER_USERNAME%/final/${appName}"
                        }
                    }
                }
            }
        }
    }
}