@Library("shared-library") _
pipeline {
    agent any
    stages {
        stage ("build") {
            when {
                branch 'develop'
            }
            steps {
                withCredentials(bindings: [
                   usernamePassword(credentialsId: "dockerhub", usernameVariable: "USER", passwordVariable: "PASSWORD")
            ])  {
                sh '''#!/bin/bash
                make docker_k8s_build;
                docker tag streamnative/apache-pulsar-grafana-dashboard-k8s:0.1.0-SNAPSHOT qraftaxe/axe-grafana:develop; 
                docker login -u $USER -p $PASSWORD
                docker push qraftaxe/axe-grafana:develop;
                docker rm -f qraftaxe/axe-grafana:develop;
                docker logout;
                '''
                } 
            }
        }
    }
}
