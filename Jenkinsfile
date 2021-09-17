pipeline {
    agent {
        label "dockerworker"
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package -f ./Jenkins-future/pom.xml'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test -f ./Jenkins-future/pom.xml'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Build image') {
            steps {
                sh 'docker build -t my-app .'
            }
        }
        stage('Run app') {
            steps {
                sh 'docker run -p my-app'
            }
        }
    }
    post {
        always {
            deleteDir()
        }
    }
}
