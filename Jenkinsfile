properties([pipelineTriggers([githubPush()])])

pipeline {
    agent { node { label 'bb41d20c7f5d' } }

    stages {
        stage('Build') {
            steps {
                echo 'Building Stuff2..'
		git 'https://github.com/mattk25/java-project.git'
		sh 'ant -f build.xml -v'
            }
        }
	    stage('Report') {
		    withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'e5c6ac1b-c40b-4453-be74-d56b3f63d231', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {]) {
			    sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins >> report.txt'
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
			sh '/usr/bin/aws s3 cp /workspace/java-pipeline/dist/rectangle-${BUILD_NUMBER}.jar s3://jenkins-s3bucket-1v6cyt3fo38f2/rectangle-${BUILD_NUMBER}.jar'
}
            }
	}
    }
}
