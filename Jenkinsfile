pipeline {
    agent any

        stage('Vérifier les DAGs Airflow') {
            steps {
                echo 'Validation syntaxique des DAGs...'
                sh 'python3 -m py_compile airflow/dags/*.py'
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

