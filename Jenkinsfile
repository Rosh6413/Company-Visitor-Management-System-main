pipeline {
    agent any

    environment {
        PHP_PATH = "/usr/bin/php"
        COMPOSER_PATH = "/usr/bin/composer"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Rosh6413/Company-Visitor-Management-System-main.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh "${COMPOSER_PATH} install"
            }
        }

        stage('Syntax Check') {
            steps {
                sh "${PHP_PATH} -l index.php"
            }
        }

        stage('Run Tests') {
            steps {
                sh "${PHP_PATH} vendor/bin/phpunit"
            }
        }

        stage('Deploy to Apache') {
            steps {
                sh '''
                sudo cp -r * /var/www/html/
                sudo systemctl restart apache2
                '''
            }
        }
    }

    post {
        success {
            echo 'Build and Deployment Successful!'
        }
        failure {
            echo 'Build Failed. Check Console Output!'
        }
    }
}

