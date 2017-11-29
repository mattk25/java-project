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
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'e5c6ac1b-c40b-4453-be74-d56b3f63d231', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
			sh '/usr/bin/aws s3 cp /workspace/java-pipeline/dist/rectangle-${BUILD_NUMBER}.jar s3://jenkins-s3bucket-1v6cyt3fo38f2.s3.amazonaws.com/rectangle-${BUILD_NUMBER}.jar'
}
            }
        }
    }
}
