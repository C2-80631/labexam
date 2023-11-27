pipeline {
    agent any

    stages {
        stage ('SCM') {
            steps {
                git branch: 'master', url: 'https://github.com/C2-80631/labexam.git'
            }
        }
        stage ('docker login') {
            steps {
                sh 'echo dckr_pat_dvWd9FEukz-2ikcZfuyKDbDfmXo | /usr/bin/docker login -u sc4458 --password-stdin'
            }
        }
        stage ('docker build image') {
            steps {
                sh '/usr/bin/docker image build -t sc4458/resume .'
            }
        }
        stage ('docker push image') {
            steps {
                sh '/usr/bin/docker image push sc4458/resume'
            }
        }
        stage ('docker remove service') {
            steps {
                sh '/usr/bin/docker service rm myservice'
            }
        }
        stage ('docker create service') {
            steps {
                sh '/usr/bin/docker service create --name myservice -p 9876:80 --replicas 5 sc4458/resume'
            }
        }
    }
}

