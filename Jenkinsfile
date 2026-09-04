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
                sh 'terraform fmt -check'
                sh 'terraform validate'
            }
        }

        stage('Terraform Init') {
            steps {
                sh 'terraform init'
            }
        }

        stage('Terraform Plan') {
            steps {
                sh 'terraform plan -out=tfplan'
            }
        }

        // ❌ No apply stage, since you don’t want to push infra
    }

    post {
        always {
            echo 'Pipeline finished. Terraform code validated successfully.'
        }
    }
}
