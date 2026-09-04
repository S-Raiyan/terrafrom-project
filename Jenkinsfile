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

        stage('Terraform Format') {
            steps {
                bat 'C:\\terraform_1.15.8_windows_386\\terraform.exe fmt -check'
            }
        }

        stage('Terraform Init') {
            steps {
                bat 'C:\\terraform_1.15.8_windows_386\\terraform.exe init'
            }
        }

        stage('Terraform Validate') {
            steps {
                bat 'C:\\terraform_1.15.8_windows_386\\terraform.exe validate'
            }
        }

        stage('Terraform Plan') {
            steps {
                bat 'C:\\terraform_1.15.8_windows_386\\terraform.exe plan -out=tfplan'
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
            echo 'Pipeline finished. Terraform code initialized, validated, and plan archived.'
        }
    }
}
