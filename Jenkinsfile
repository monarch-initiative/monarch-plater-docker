pipeline {
    agent any
    stages {
        stage('build-container') {
            steps {
                sh 'docker build --tag plater-dev .'
                sh 'docker tag plater-dev us-central1-docker.pkg.dev/monarch-initiative/monarch-initiative/plater-sri:dev'
                sh 'docker push us-central1-docker.pkg.dev/monarch-initiative/monarch-initiative/plater-sri:dev'
            }
        }
        stage('gcp-deploy') {
            steps {
                sh 'gcloud compute instances update-container monarch-trapi --container-image=us-central1-docker.pkg.dev/monarch-initiative/monarch-initiative/plater-sri:dev'
            }
        }
    }
}