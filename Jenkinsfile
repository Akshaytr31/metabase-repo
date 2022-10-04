pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('55c486b3-36d6-4d67-aa50-9a39ee10e3b2')
	}

	stages {
	    
	    stage('gitclone') {

			steps {
				git 'https://github.com/Akshaytr31/metabase-repo.git'
			}
		}

		stage('Build') {

			steps {
				sh 'docker build -t akshaytr123/mysql:latest .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push akshaytr123/mysql:latest'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}
