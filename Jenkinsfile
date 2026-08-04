pipeline {

    agent {
        label 'agent1'
    }

    stages {

        stage('Clean') {
            steps {
                cleanWs()
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    cd ansible
                    ANSIBLE_CONFIG=ansible.cfg \
                    ansible-playbook playbooks/deploy.yml
                '''
            }
        }
    }
}