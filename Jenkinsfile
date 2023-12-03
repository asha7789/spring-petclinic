pipeline {
    agent { label 'MAVEN' }
    tools { 
        maven 'Maven 3.9.5'
    }
    options { 
        timeout(time: 30, unit: 'MINUTES') 
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
                archiveArtifacts artifacts: '**/spring-petclinic-*.jar'
                junit testResults: '**/TEST-*.xml'
            }
        }
    }

}
