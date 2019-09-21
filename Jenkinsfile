pipeline {
    agent {
        # указываем, что выполнять задачу хотим внутри 
        # Docker-контейнера на базе указанного образа:
        docker {
            image 'centos:centos7.6.1810'
        }
    }
    
    stages {
        stage('Стягиваем код из ГИТа') {
            steps {
                checkout scm
            }
        }
        stage('Собираем') {
            steps {
                echo env.BRANCH_NAME
                sh 'echo $env.BRANCH_NAME'
            }
 
        }
        stage('Тестируем') {
            steps {
                script {
                    sh 'uname -a'
                }
            }
        }
    }
}
 
