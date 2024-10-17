pipeline {
    agent any

    tools {
        jdk 'JDK 11'
    }

    stages {
        stage('Build') {
            steps {
                sh './mvnw clean install'
            }
        }

        stage('Run Tests and Generate Jacoco Coverage') {
            steps {
                sh './mvnw test jacoco:report'
            }
            post {
                always {
                    jacoco execPattern: 'target/jacoco.exec', classPattern: 'target/classes', sourcePattern: 'src/main/java', exclusionPattern: ''
                }
            }
        }

    }

    triggers {
        // Run every 10 minutes on Mondays
        cron('H/10 * * * 1')
    }
}
