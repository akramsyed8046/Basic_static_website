pipeline {


agent any

stages {

    stage('Clone') {
        steps {
            git branch: 'main',
                url: 'https://github.com/akramsyed8046/Basic_static_website.git'
        }
    }

    stage('Build Docker Image') {
        steps {
            sh 'docker rmi -f static-website || true'
            sh 'docker build -t static-website .'
        }
    }

    stage('Update Kubeconfig') {
        steps {
            sh '''
                aws eks update-kubeconfig \
                    --region ap-south-1 \
                    --name Enterprises
            '''
        }
    }

    stage('Verify EKS Connection') {
        steps {
            sh '''
                kubectl config current-context
                kubectl get nodes
            '''
        }
    }

    stage('Deploy to EKS') {
        steps {
            sh 'kubectl apply -f deployment.yaml'
        }
    }

}


}
