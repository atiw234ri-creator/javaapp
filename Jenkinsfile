pipeline {

    agent {
        label 'agent1'
    }

    stages {

        stage('Build') {
            steps {
                sh '''
                    echo "Current Directory:"
                    pwd

                    echo "Repository Files:"
                    ls -la

                    echo "Building Application..."

                    cd app
                    mvn clean package
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    echo "Deploying with Ansible..."

                    cd ansible

                    ANSIBLE_CONFIG=ansible.cfg \
                    ansible-playbook playbooks/deploy.yml
                '''
            }
        }
    }
}