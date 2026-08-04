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

                    echo "Finding pom.xml:"
                    find . -name pom.xml

                    mvn clean package
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    echo "Ansible Directory:"
                    ls -la ansible

                    cd ansible

                    ANSIBLE_CONFIG=ansible.cfg \
                    ansible-playbook playbooks/deploy.yml
                '''
            }
        }
    }
}