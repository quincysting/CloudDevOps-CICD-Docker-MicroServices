pipeline {
	agent any
	stages {

		stage('Create kubernetes cluster') {
			steps {
				withAWS(region:'us-west-2', credentials:'Mypass') {
					sh '''
						eksctl create cluster \
						--name proj5cluster \
						--version 1.13 \
						--nodegroup-name proj5-nodes \
						--node-type t2.small \
						--nodes 2 \
						--nodes-min 1 \
						--nodes-max 3 \
						--node-ami auto \
						--region us-west-2 \
						--zones us-west-2a \
						--zones us-west-2b \
						--zones us-west-2c \
					'''
				}
			}
		}

		stage('Create cluster config file') {
			steps {
				withAWS(region:'us-west-2', credentials:'Mypass') {
					sh '''
						aws eks --region us-west-2 update-kubeconfig --name proj5cluster
					'''
				}
			}
		}

	}
}
