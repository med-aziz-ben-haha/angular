pipeline {
  agent any
    stages {
        stage('Pull') {
             steps{
                script{
                    checkout([$class: 'GitSCM', branches: [[name: '*/main']],
                        userRemoteConfigs: [[
                            url: 'https://github.com/med-aziz-ben-haha/angular.git']]])
                }
            }
        }
        stage('Install') {
             steps{
                script{
                    sh "npm install"
                }
            }
        }
        stage('Build') {
             steps{
                script{
                    sh "ansible-playbook ansible/build.yml -i ansible/inventory/host.yml"
                }
            }
        }
        stage('Docker') {
             steps{
                script{
                    sh "ansible-playbook ansible/docker.yml -i ansible/inventory/host.yml"
                }
            }
        }
        stage('DockerHub push') {
             steps{
                script{
                    sh "ansible-playbook ansible/docker-registry.yml -i ansible/inventory/host.yml"
                }
            }
        }
       }
      }
