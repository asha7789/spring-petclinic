pipeline {
    agent { label 'MAVEN' }
    options (time: 30, unit: 'MINUTES')
    }
    triggers {
        pollSCM('* * * * *')
    }
    stages {
        stage('git') {
            steps {
                git url: 'https://github.com/asha7789/spring-petclinic.git',
                branch: 'dev'
         }
        }
        stage('build') {
            steps {
                sh 'mvn clean package'
            }
        }
    }
}
