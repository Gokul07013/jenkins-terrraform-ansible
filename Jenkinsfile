pipeline {
    agent any
    
    environment{
        
        PATH = "${env.PATH}:/opt/homebrew/bin"
        location_key = "/Users/gokul/Downloads/virginia.pem"
    }    

    stages {
        stage('Git checkout') {
            steps {
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/Gokul07013/jenkins-terrraform-ansible'
            }
        }
        
        stage('Terraform aws resource creation') {
            steps {
                sh '''terraform init
                      terraform plan
                      terraform validate
                      terraform apply -auto-approve
                   '''    
            }
        }
        
        stage('Ansible configuration') {
            steps {
               sh"ansible-playbook -i inventory.ini --private-key ${location_key} nginx-service.yaml" 
            }
        }
  
        
    }
}
