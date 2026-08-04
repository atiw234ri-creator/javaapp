pipeline {

    agent {
        label 'agent1'
    }

    stages {

        stage('Build') {
            steps {
                sh '''
                    set -e

                    echo "Building Java Application..."

                    cd app

                    mvn clean package

                    echo "Generated JAR:"
                    ls -lh target/
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    set -e

                    echo "Deploying with Ansible..."

                    cd ansible

                    ANSIBLE_CONFIG=ansible.cfg \
                    ansible-playbook \
                    -i inventory/hosts.ini \
                    playbooks/deploy.yml
                '''
            }
        }
    }
}