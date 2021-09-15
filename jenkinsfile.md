pipeline {
    agent any
    environment {
        BARCREATION = "/opt/ace-11.0.0.7/tools/mqsicreatebar"
        DATA = "/home/bandaru/Desktop/docker/docker/bars/"
        bar = "/home/bandaru/Videos"
        Nexus_repository = "http://localhost:8081/repository/devops/"
        Docker = "/home/bandaru/Desktop/docker/docker/"
        oc = "/usr/local/bin"
        shell = "/home/bandaru/Desktop"
        job = "devops_cicd"
    }
    stages {
        stage('Building Bar File') {
            steps {
                sh 'echo Building Bar'
                git branch: 'main', url: 'https://github.com/manojawsdevops/Poc-devops.git'
                sh '$BARCREATION -data $WORKSPACE -b $bar/$job-$BUILD_NUMBER.bar -a Application1'
            }
        }
        stage('Publishibg') {
            steps {
                sh 'echo Publishing Bar File To Nexus Repository'
                withCredentials([usernamePassword(credentialsId: 'c88ef86f-fa48-4c38-9a7d-f618061999d5', passwordVariable: 'password', usernameVariable: 'username')]) {
                sh 'curl -v -uadmin:admin --upload-file $bar/$job-$BUILD_NUMBER.bar $Nexus_repository'
                }
            }
        }
        stage('Artifacts') {
            steps {
                sh 'echo Automation'
                withCredentials([usernamePassword(credentialsId: 'c88ef86f-fa48-4c38-9a7d-f618061999d5', passwordVariable: 'password', usernameVariable: 'username')]) {
                sh 'cd $DATA && rm -rf *.bar && wget $Nexus_repository/$job-$BUILD_NUMBER.bar --user=admin --password=admin && chmod -R 777 *'
                }
            }
        }
        stage('Docker Build') {
            steps {
                sh 'echo Docker image building'
                sh 'cd $Docker && docker build -f dockerfile -t bharathmanikanta1997/devops:v1 .'
                emailext body: '$JOB_URL', recipientProviders: [developers()], subject: 'EIDIKO_POC', to: 'manojkumar14370@gmail.com'
                input 'Ready to Deploy'
                withCredentials([usernamePassword(credentialsId: '3d1f25e6-30d3-4b84-84c5-37169ee05270', passwordVariable: 'oc_password', usernameVariable: 'oc_username')]) {
                sh 'cd $oc && ./oc login -u kubeadmin -p a93h8-5RDhQ-KU63X-4tskh --insecure-skip-tls-verify=true'
                sh 'cd $oc && ./oc project dev1'
                withCredentials([usernamePassword(credentialsId: 'c88ef86f-fa48-4c38-9a7d-f618061999d5', passwordVariable: 'Docker_Password', usernameVariable: 'Docker_Username')]) {
                sh 'docker login -u bharathmanikanta1997 -p Bharath@123'
                sh 'docker push bharathmanikanta1997/devops:v1'
                sh '/home/bandaru/Desktop/devshift.sh'
                }
             }
            }
        }
    }
}
