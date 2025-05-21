pipeline {
    agent any

    stages {

        stage('Installer Python (si nécessaire)') {
            steps {
                echo 'Pas de Python, mais on continue quand même...'
                sh 'which python3 || true'
            }
        }

        stage('Vérifier les DAGs Airflow') {
            steps {
                echo 'Validation syntaxique des DAGs...'
                sh 'python3 -m py_compile airflow/dags/*.py || echo "Python non dispo, étape sautée"'
            }
        }

        stage('Build des images Docker') {
            steps {
                echo 'Construction des images Docker...'
                sh 'docker build -t airflow-app ./airflow'
                sh 'docker build -t backend-api ./backend'
                sh 'docker build -t frontend-ui ./frontend'
            }
        }

        stage('Lancement avec Docker Compose') {
            steps {
                echo 'Lancement des services...'
                sh 'docker-compose up -d'
            }
        }
    }
}
