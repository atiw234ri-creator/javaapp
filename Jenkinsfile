pipeline {

    agent {
        label 'agent1'
    }

    stages {

        

        stage('Build') {
            steps {
                sh '''
                    ls -la
                    find . -name pom.xml
                    cd app
                    mvn clean package
                '''
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