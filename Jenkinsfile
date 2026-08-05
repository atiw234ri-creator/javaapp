pipeline {

    agent {
        label 'agent1'
    }

    tools {
        jdk 'jdk17'
        maven 'Maven3'
    }

    environment {
        SONAR_HOME = tool 'SonarScanner'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Validate') {
            steps {
                dir('app') {
                    sh 'mvn validate'
                }
            }
        }

        stage('Compile') {
            steps {
                dir('app') {
                    sh 'mvn compile'
                }
            }
        }

        stage('Test') {
            steps {
                dir('app') {
                    sh 'mvn test'
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                dir('app') {
                    withSonarQubeEnv('SonarQube') {
                        sh '''
                            mvn sonar:sonar \
                            -Dsonar.projectKey=java-app \
                            -Dsonar.projectName=java-app
                        '''
                    }
                }
            }
        }

        stage('Quality Gate') {
            steps {
                timeout(time: 5, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }

        stage('Package') {
            steps {
                dir('app') {
                    sh '''
                        echo "Packaging Application..."
                        mvn package

                        echo "Generated JAR:"
                        ls -lh target/
                    '''
                }
            }
        }

        stage('Publish to Nexus') {
            steps {
                dir('app') {
                    sh '''
                        echo "Uploading JAR to Nexus..."
                        mvn deploy
                    '''
                }
            }
        }

    }

    post {

        success {
            echo "CI Pipeline Completed Successfully."
        }

        failure {
            echo "CI Pipeline Failed."
        }

    }

}