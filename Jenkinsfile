pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/S-Raiyan/terrafrom-project.git',
                    credentialsId: 'github-creds'
            }
        }

        stage('Terraform Format & Validate') {
            steps {
                bat 'terraform fmt -check'
                bat 'terraform validate'
            }
        }

        stage('Terraform Init') {
            steps {
                bat 'terraform init'
            }
        }

        stage('Terraform Plan') {
            steps {
                bat 'terraform plan -out=tfplan'
            }
        }

        stage('Archive Plan') {
            steps {
                archiveArtifacts artifacts: 'tfplan', fingerprint: true
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished. Terraform code validated and plan archived.'
        }
    }
}
