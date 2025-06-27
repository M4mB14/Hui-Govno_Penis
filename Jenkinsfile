pipeline {
  agent { node {
    label 'agent2'
  } }

  environment{
    MY_TOKEN = credentials('yc_token')
    MY_CLOUD_ID = credentials('yc_cloud_id')
    MY_FOLDER_ID = credentials('yc_folder_id')
    SUBNET_ID = credentials('subnet_id')
    SSH_PATH = credentials('ssh_public_key_path')
  }
  stages {
    stage('SSH key generate') {
      steps {
        sh '''
        rm -f jenkins jenkins.pub
        ssh-keygen -t rsa -b 4096 -C "jenkins@ci" -N "" -f jenkins 
        '''
      }
    }

    stage('Create tf.vars file') {
      steps {
        sh '''
          cd terraform &&\
          rm -f terraform.tfvars && touch terraform.tfvars && \
          printf 'yc_token = "%s"\n' "$MY_TOKEN" >> terraform.tfvars && \
          printf 'yc_cloud_id = "%s"\n' "$MY_CLOUD_ID" >> terraform.tfvars && \
          printf 'yc_folder_id = "%s"\n' "$MY_FOLDER_ID" >> terraform.tfvars && \
          printf 'subnet_id = "%s"\n' "$SUBNET_ID" >> terraform.tfvars && \
          printf 'ssh_public_key_path = "%s"\n' "$SSH_PATH" >> terraform.tfvars

        '''
      }
    }
    stage('Terraform init and Ansible inventory init') {
      steps {
        sh '''
        cd terraform &&\
        terraform init &&\
        terraform plan &&\
        terraform apply --auto-approve &&\
        VM_IP=$(terraform output -raw vm_ip) &&\

        cd ../ansible &&\
        echo "[vm]" > ./inventory.ini &&\
        echo "$VM_IP ansible_user=ubuntu ansible_ssh_private_key_file=~/workspace/test-job/jenkins" >> ./inventory.ini
        '''
      }
    }

        stage('Ansible run'){
      steps {
        sh '''
        cd ansible &&\
        ansible-playbook -i inventory.ini site.yml
        '''
      }
    }
  }
}
