pipeline {
    agent { label 'MAVEN' }
    tools { 
        maven 'MAVEN_3.9.5'
    }
    options { 
        timeout(time: 30, unit: 'MINUTES') 
    }
    triggers {
        cron('30 16 * * *')
    }
    stages {
        stage('git') {
            steps {
                git url: 'https://github.com/asha7789/spring-petclinic.git',
                branch: 'release'
         }
        }
        stage('build') {
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    archiveArtifacts artifacts: '**/spring-petclinic-*.jar'
                    junit testResults: '**/TEST-*.xml'
                    mail subject: 'build stage succeeded',
                        from: 'build@testdevops.io',
                        to: 'all@testdevops.io',
                        body: "Refer to $BUILD_URL for more details"
                }
                failure {
                    mail subject: 'build stage failed',
                        from: 'build@testdevops.io',
                        to: 'all@testdevops.io',
                        body: "Refer to $BUILD_URL for more details"
                }
            }
        }
    }

}
