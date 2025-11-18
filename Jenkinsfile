pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Ejecucion de Tests') {
            steps {
                sh '''
                cd app
                pytest
                '''
            }
        }

        stage('Ejecucion de Terraform Init/Apply') {
            steps {
                sh '''
                cd terraform
                terraform init
                terraform apply -auto-approve -var="private_key_path=/home/ubuntu/key.pem"
                '''
            }
        }

        stage('Generar Inventory') {
            steps {
                sh '''
                cd ansible
                PUBLIC_IP=$(cat ip.txt)
                echo "[app]" > inventory
                echo "$PUBLIC_IP ansible_user=ubuntu ansible_ssh_private_key_file=/home/ubuntu/key.pem" >> inventory
                '''
            }
        }

        stage('Deploy con Ansible') {
            steps {
                sh '''
                cd ansible
                ansible-playbook -i inventory playbook.yml
                '''
            }
        }
    }
}
🟩 5. README.