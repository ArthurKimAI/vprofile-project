pipeline{
    agent any
    tools{
        maven "MAVEN3"
        jdk "OracleJDK8"
    }

    // Variables for pom.xml file
    environment{
        SNAP_REPO = 'vprofile-snapshot'
        NEXUS_USER = 'admin'
        NEXUS_PASS = 'admin123'
        RELEASE_REPO = 'vprofile-release'
        CENTRAL_REPO = 'vpro-maven-central'
        NEXUSIP = '172.31.5.4'
        NEXUSPORT = '8081'
        NEXUS_GRP_REPO = 'vpro-maven-group'
        NEXUS_LOGIN = 'nexuslogin'

    }
    stages{
        stage('Build'){
            steps{
                sh 'mvn -s setting.xml -DskipTests install'
            }
        }

        post{
            success {
                echo "Now Archiving"
                archiveArtifacts artifacts: '**/*.war'
            }
        }
    }

    stage('Test') {
        steps {
            sh 'mvn setting.xml test'
        }
    }

    stage('Checkstyle Analysis') {
        steps {
            sh 'mvn setting.xml checkstyle:checkstyle'
        }
    }
}