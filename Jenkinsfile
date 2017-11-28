properties([pipelineTriggers([githubPush()])])

pipeline {
    agent any


    stages {
        stage('Build') {
            steps {
                echo 'Building Stuff..'
		git 'https://github.com/mattk25/java-project.git'
		sh 'ant -buildfile test.xml'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
