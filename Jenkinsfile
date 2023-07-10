pipeline {
  agent any
  stages {
    stage('Code checkout') {
      steps {
        git(url: 'https://github.com/<ManyaBM>/<majorproject>', branch: 'main')
      }
    }

    stage('Test') {
      steps {
        echo 'Starting unittests'
        sh 'export DATABASE_URL=sqlite:///restaurant.db && pip3 install -r requirements.txt && pip3 install nose && nosetests --with-xunit'
      }
    }

    stage('Build') {
      steps {
        sh '''echo $USER
'''
        sh 'docker build -t manyabm/restuarant_management_app:latest .'
      }
    }

    stage('Deploy') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerhubcredentials', usernameVariable: 'DOCKERHUB_USERNAME', passwordVariable: 'DOCKERHUB_PASSWORD')]) {
          sh 'docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD'
          sh 'docker push manyabm/restuarant_management_app:latest'
        }
      }
    }
  }
}
