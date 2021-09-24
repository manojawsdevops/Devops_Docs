name: Docker Image CI
        
on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:

  build:

    runs-on: self-hosted

    steps:
    - uses: actions/checkout@v2
    - name: docker login
      env:
        DOCKER_USER: ${{secrets.DOCKER_USER}}
        OC_USERNAME: ${{secrets.OC_USERNAME}}
        OC_PASSWORD: ${{secrets.OC_PASSWORD}}
      run: |
        docker login -u $DOCKER_USER --password $(oc whoami -t) default-route-openshift-image-registry.apps.ocp4.eidikointernal.com
    - name: Build the Docker image
      run: docker build -t firstimage:v1 --file dockerfilenew . 
    - name: oc login,oc project,Docker tag & Docker push
      run: |
        /usr/local/bin/ && ./oc login -u $OC_USERNAME -p $OC_PASSWORD --insecure-skip-tls-verify=true
        /usr/local/bin/ && ./oc project manojprod
        docker tag firstimage:v1 default-route-openshift-image-registry.apps.ocp4.eidikointernal.com/manojprod/devopsimage:v1
        docker push default-route-openshift-image-registry.apps.ocp4.eidikointernal.com/manojprod/devopsimage:v1
        /home/bandaru/Downloads/devshift.sh
