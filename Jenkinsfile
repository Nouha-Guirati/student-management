pipeline {
    agent any
    stages {
        stage('Checkout GIT') {
            steps {
                echo 'Pulling...'
                git branch: 'main',
                    url: 'https://github.com/Nouha-Guirati/student-management.git'
            }
        }
        stage('Testing maven') {
            steps {
                sh 'mvn -version'
            }
        }
        stage('MVN CLEAN') {
            steps {
                sh 'mvn clean'
            }
        }
        stage('MVN COMPILE') {
            steps {
                sh 'mvn compile'
            }
        }
      stage('Deploy on Kubernetes') {
    steps {
        sh '''
            kubectl apply -f /home/vagrant/hello-k8s/namespace.yaml || true
            kubectl apply -f /home/vagrant/hello-k8s/mysql-deployment.yaml -n devops || true
            kubectl apply -f /home/vagrant/hello-k8s/spring-configmap.yaml -n devops || true
            kubectl apply -f /home/vagrant/hello-k8s/spring-secret.yaml -n devops || true
            kubectl apply -f /home/vagrant/hello-k8s/spring-deployment.yaml -n devops || true
            kubectl apply -f /home/vagrant/hello-k8s/spring-service.yaml -n devops || true
        '''
    }
}
        stage('MVN SONARQUBE') {
            steps {
                sh 'mvn sonar:sonar -Dsonar.host.url=http://192.168.50.4:9000 -Dsonar.login=admin -Dsonar.password=sonar'
            }
        }
    }
}
