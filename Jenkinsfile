    agent any

    stages {
        stage('kubectl') {
            steps {
                sh '''
                kubectl create deploy pytest --image=sanjidakram/devpython --dry-run=client -o yaml > deployment.yaml
                kubectl apply -f deployment.yaml
                kubectl expose deploy pytest --name=pytest-svc --type=NodePort --port=5009 --target-port=5000 --dry-run=client > service.yaml
                kubectl apply -f service
            }
        }
    }
}
