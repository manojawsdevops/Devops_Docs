pipeline {
    agent any
    environment {
        BARCREATION = "/opt/ace-11.0.0.7/tools/mqsicreatebar"
        DATA = "/home/bandaru/Desktop/docker/docker/bars/"
        bar = "/home/bandaru/Videos"
        Nexus_repository = "http://localhost:8085/repository/devops_cicd/"
        Docker = "/home/bandaru/Desktop/docker/docker/"
        oc = "/usr/local/bin"
        job = "Devops_RakCICD"
    }
    stages {
        stage('Building Bar File') {
            steps {
                sh 'echo Building Bar'
                git branch: 'main', url: 'https://github.com/manojawsdevops/Devops_RakCICD.git'
                sh '$BARCREATION -data $WORKSPACE -b $bar/$job-$BUILD_NUMBER.bar -a Application1'
            }
        }
        stage('Publishing') {
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
                sh 'cd $Docker && docker build -f dockerfile -t manojreddyeidiko/devopsprod:v1 .'
                emailext body: '$JOB_URL', recipientProviders: [developers()], subject: 'EIDIKO_POC', to: 'manojkumar14370@gmail.com'
                input 'Ready to Deploy'
                sh 'cd $oc && ./oc login -u kubeadmin -p r6PzC-4hayC-TjCIg-NaL4m --insecure-skip-tls-verify=true'
                sh 'cd $oc && ./oc project manoj'
                sh 'docker login -u manojreddyeidiko -p Ashwanth@8801'
                sh 'docker push manojreddyeidiko/devopsprod:v1'
                sh '/home/bandaru/Desktop/devshift.sh'
                }
             
            }
        }
    }
