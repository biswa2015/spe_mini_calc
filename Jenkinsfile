
pipeline {
    agent any
    environment {
        imageName = ""
    }
    stages {
        stage('Step 1 Git') {
            steps {
                git 'https://github.com/biswa2015/spe_mini_calc.git'
            }
        }
         stage('Step 2 Maven') {
            steps {
                 sh 'mvn clean install'
            }
        }
         stage('Step 3 Docker_Image')
          {
              steps {
                  script {
                    imageName = docker.build "biswa2015/spe_mini:calc_devops"
                    }
              }
          }
         stage('Step 4 Push Docker Image')
        {
            steps {
                script{
                  docker.withRegistry('', 'dockerhub-cred-biswa') {
                       imageName.push()
                  }
                }
            }
        } 
        stage('Step 5 Ansible'){
            steps{
                ansiblePlaybook becomeUser: null, colorized: true, disableHostKeyChecking: true, installation: 'Ansible', inventory: 'inventory', playbook: 'playbook.yml', sudoUser: null
            }
        }
    }   
}
