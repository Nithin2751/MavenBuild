pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/Nithin2751/MavenBuild.git', branch: 'master'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install -Dmaven.test.skip=true'
            }
        }

        stage('Test Cases Execution') {
            steps {
                sh 'mvn clean org.jacoco:jacoco-maven-plugin:prepare-agent install -Pcoverage-per-test'
            }
        }

        

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.war', fingerprint: true
            }
        }

        stage('Deployment') {
    steps {
        withCredentials([usernamePassword(credentialsId: 'TomcatCreds', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
            sh '''
                curl -v --upload-file target/*.war \
                "http://$USER:$PASS@54.167.173.84:8080/manager/text/deploy?path=/controlplane&update=true"
            '''
        }
    }
}


        
    }
}
