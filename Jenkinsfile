
pipeline {

agent {

label 'agent1'

}

environment {

VAULT="/tmp/vault_pass.txt"

}

stages {

stage('Clean'){

steps{

cleanWs()

}

}

stage('Checkout'){

steps{

git branch: 'main',

url: 'https://github.com/username/gitops-demo.git',

credentialsId: 'github-token'

}

}

stage('Build'){

steps{

sh 'mvn clean package'

}

}

stage('Vault'){

steps{

withCredentials([string(credentialsId:'vault-pass',

variable:'PASSWORD')]){

sh '''

echo $PASSWORD > $VAULT

'''

}

}

}

stage('Deploy'){

steps{

sh '''

cd ansible

ANSIBLE_CONFIG=ansible.cfg \

ansible-playbook playbooks/deploy.yml \

--vault-password-file=$VAULT

'''

}

}

}

post{

always{

sh 'rm -f /tmp/vault_pass.txt'

}

}

}
