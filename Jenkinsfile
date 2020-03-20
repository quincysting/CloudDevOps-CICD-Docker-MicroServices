pipeline {
	agent any
	stages {

		stage('Lint HTML') {
			steps {
				sh 'tidy -q -e *.html'
			}
		}
		
		stage('Build Docker Image') {
			steps {
				withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD']]){
					sh '''
						docker build -t quincysting/project5 .
					'''
				}
			}
		}

		stage('Push Image To Dockerhub') {
			steps {
				withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD']]){
					sh '''
						docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD
						docker push quincysting/project5
					'''
				}
			}
		}

		stage('Set current kubectl context') {
			steps {
				withAWS(region:'us-west-2', credentials:'Mypass') {
					sh '''
						kubectl config use-context arn:aws:eks:us-west-2:570781860922:cluster/proj5cluster
						kubectl get services
					'''
				}
			}
		}

		stage('Deploy blue container') {
			steps {
				withAWS(region:'us-west-2', credentials:'Mypass') {
					sh '''
						kubectl apply -f ./blue-controller.json
					'''
				}
			}
		}

		stage('Deploy green container') {
			steps {
				withAWS(region:'us-west-2', credentials:'Mypass') {
					sh '''
						kubectl apply -f ./green-controller.json
					'''
				}
			}
		}

		stage('Create service in the cluster, redirect to blue') {
			steps {
				withAWS(region:'us-west-2', credentials:'Mypass') {
					sh '''
						kubectl apply -f ./blue-service.json
					'''
				}
			}
		}

		stage('Wait approval') {
            steps {
                input "Ready to redirect traffic to green?"
            }
        }

		stage('Create service in the cluster, redirect to green') {
			steps {
				withAWS(region:'us-west-2', credentials:'Mypass') {
					sh '''
						kubectl apply -f ./green-service.json
					'''
				}
			}
		}

	}
}
