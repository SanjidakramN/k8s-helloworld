@Library('pytest') _
pipeline {
    agent any

    stages {
        stage('build') {
            steps {
                sh '''
                docker build -t sanjidakram/devpython .
                if (docker ps -a | grep devpython)
                then
                    docker stop devpython
                    docker rm devpython
                fi
                docker run -d -p 5009:500 --name devpython sanjidakram/devpython
                '''
            }
        }
        stage('login') {
            steps {
            pyTest()
            withCredentials([usernamePassword(credentialsId: 'docker-cred', passwordVariable: 'password', usernameVariable: 'username')]) {
                sh '''
                docker login -u $username -p $password
                docker push sanjidakram/devpython
                sh '''
            }
        }
    }
}
}
