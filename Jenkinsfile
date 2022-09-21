pipeline {
    agent any

    stages {
        stage('check-out') {
            steps {
                sh 'git clone git@github.com:purnasaiab/sparkjava-war-example.git'
            }
        }
        stage('mvn package') {
            steps {
                sh '/opt/maven386/bin/mvn clean package'
            }
        }
         stage('ci process') {
            steps {
                sh 'mv target/sparkjava-hello-world-1.0.war target/sparkjava-hello-world-$BUILD_NUMBER.war'
                sh 'aws s3 cp target/sparkjava-hello-world-$BUILD_NUMBER.war s3://artifactoty-java'
            }
        }
        stage('cd process') {
            steps {
                sh 'aws s3 cp s3://artifactoty-java/sparkjava-hello-world-$PKG.war .'
                sh 'scp -r sparkjava-hello-world-$PKG.war root@172.31.11.49:/opt/tomcat9/webapps'
            }
        }
    
    
    }

}
