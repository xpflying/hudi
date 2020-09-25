pipeline {
    agent { node { label 'master' } }
    options {
        buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '30', numToKeepStr: '10')
        ansiColor('xterm')
        timestamps()
    }


    stages {  
        stage('deploy') {
            agent {
                docker { image 'reg.leadswarp.com/base/maven:3-openjdk-8' }
            }  
            steps {
                sh 'mvn deploy -DskipTests -Prelease -Dgpg.skip -pl packaging/hudi-spark-bundle,packaging/hudi-hadoop-mr-bundle -am'
            }
        }
    }
    post { 
        always { 
            cleanWs()
        }
    }
}
