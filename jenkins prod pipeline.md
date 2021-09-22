pipeline {
    agent any
    environment {
        oc = "/usr/local/bin"
    }
    stages {
        stage('Docker Build') {
            steps {
                sh 'echo Docker image building'
                input 'Deploying to prod?'
                sh 'cd $oc && ./oc login -u kubeadmin -p r6PzC-4hayC-TjCIg-NaL4m --insecure-skip-tls-verify=true'
                sh 'cd $oc && ./oc project manojprod'
                sh 'docker login -u manojreddyeidiko --password Ashwanth@8801'
                sh 'docker push manojreddyeidiko/devopsprod:v1'
                sh '/home/bandaru/Desktop/prodshift.sh'
            }
        }
    }
}
