pipeline {
    agent any
    environment {
         BARCREATION = "/opt/ace-11.0.0.7/tools/mqsicreatebar"
         bar = "/home/bandaru/Videos"
         job = "Application"
    }
    stages {
        stage ("Git cloning") {
            steps {
                buildName "${Application}"
                git branch: 'main', url: 'https://github.com/Tkumar84/devops.git'
            }
        }
        stage ("Building BAR fie") {
            steps {
                sh "cd $bar && rm -rf *.bar"
                sh '$BARCREATION -data $WORKSPACE -b $bar/$Application.bar -a $Application'
            }
        }
        stage ("Docker image building") {
            steps {
                sh 'docker rmi -f $(docker images -aq)'
                sh "cd /home/bandaru/Videos/ && docker build -t $JOB_NAME$BUILD_NUMBER:v1 -f dockerfile ."
                emailext body: 'Your job was sucessss', recipientProviders: [buildUser()], subject: 'hi', to: 'manojreddypentaredy@gmail.com'
                
            }
        }
        stage ("oc Login") {
            steps {
                sh "oc login -u ocpadmin -p 123456"
                sh "oc project manoj"
            }
        }
        stage ("Logging Openshift internal registry") {
            steps {
                sh 'docker login -u kubeadmin -p $(oc whoami -t) default-route-openshift-image-registry.apps.ocp4.eidikointernal.com'
                sh 'docker tag $JOB_NAME$BUILD_NUMBER:v1  default-route-openshift-image-registry.apps.ocp4.eidikointernal.com/manoj/$JOB_NAME$BUILD_NUMBER:v1'
                sh 'docker push default-route-openshift-image-registry.apps.ocp4.eidikointernal.com/manoj/$JOB_NAME$BUILD_NUMBER:v1'
            }
        }
        stage ("Deploying Application in Openshift") {
            steps {
                sh 'oc delete po -l labelname=sample -n manoj'
            //    sh 'oc delete  $JOB_NAME'
                sh 'oc new-app --docker-image=image-registry.openshift-image-registry.svc:5000/manoj/$JOB_NAME$BUILD_NUMBER:v1 -e LICENSE=accept'
                sh 'oc expose service $JOB_NAME$BUILD_NUMBER -l name=sample --port=7800'
            }
        }
       
    }
}


