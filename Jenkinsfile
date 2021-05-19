pipeline {
    agent any
    stages {
       stage('scm') {
           steps {
               git 'https://github.com/Raghu-acer/docker-helloworld.git'
           }
       }
       stage('buld') {
           steps {
               sh 'mvn clean package'
           }
       }
       stage('artifactory') {
           steps {
               archiveArtifacts 'webapp/target/*.war'
           }
       }
       stage('docker build') {
           steps {
               sh 'sudo docker image build . -t raghudusa/helloworld:19052021'
           }
       }
       stage('docker login') {
           steps {
               sh 'sudo docker login -u raghudusa -p RAGHU@123'
           }
       }
       stage('docker push') {
           steps {
               sh 'sudo docker push raghudusa/helloworld:19052021'
           }
       }
       stage('deploy ansible') {
           steps {
               ansiblePlaybook credentialsId: 'playbook', disableHostKeyChecking: true, installation: 'ansible', inventory: 'host', playbook: 'docker-hello.yaml'
           }
       }
    }
}