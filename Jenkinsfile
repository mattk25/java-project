properties([pipelineTriggers([githubPush()])])

pipeline {
    agent any


    stages {
        stage('Build') {
            steps {
                echo 'Building Stuff2..'
		git 'https://github.com/mattk25/java-project.git'
		sh 'ant -f build.xml -v'
            }
        }
        stage('Unit Tests') {
            steps {
                echo 'Testing..'
                sh 'ant -f test.xml -v'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
		aws s3 cp dist/rectangle-2.jar s3://jenkins-s3bucket-1v6cyt3fo38f2.s3.amazonaws.com/rectangle-2.jar
            }
        }
    }
}
