pipeline {
    agent any  // Запуск на любом доступном агенте
    environment {
        // Установка переменных среды, если нужно
       PATH = "/usr/local/go/bin:$PATH"
    }
    stages {
        stage('Checkout') {
            steps {
                // Клонирование репозитория

                git url:'https://github.com/vorart2004/ci-cd-hometask-voroshilov', branch: 'main'
            }
        }
        stage('Install Go') {
            steps {
                script {
                    // Убедитесь, что Go установлен
                    sh 'go version || sudo apt-get install golang-go'
                }
            }
        }
        stage('Run Tests') {
            steps {
                // Выполнение тестов Go
                script {
                    // Переходим в директорию, где находятся файлы Go (если это необходимо)
                    sh 'go test .'
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                // Построение Docker-образа
                script {
                    sh 'docker build .'
                }
            }
        }
    }
    post {
        always {
            // Этот блок выполняется всегда, например для очистки
            echo 'Cleaning up...'
        }
        success {
            // Этот блок выполняется при успешной сборке
            echo 'Build was successful!'
        }
        failure {
            // Этот блок выполняется при ошибке
            echo 'Build failed!'
        }
    }
}
