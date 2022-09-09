# name: RakBank_CICD

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]
  workflow_dispatch:
  
env: 
 OC_TOKEN: ${{secrets.OC_TOKEN}}
 OC_SERVER: ${{secrets.OC_SERVER}}
 oc_USERNAME: ${{secrets.oc_USERNAME}}
 oc_PASSWORD: ${{secrets.oc_PASSWORD}}
 oc_login: ${{secrets.oc_login}}  

jobs:
  Build:
    runs-on: self-hosted
    steps:
      - uses: actions/checkout@v2
      
      - name: oc login & deployment in ACE1
        run: cd /usr/local/bin/ && ./oc login $OC_SERVER -u $oc_USERNAME -p $oc_PASSWORD &&  ./oc project cp4i  && pwd
         
  DeployDev:
    name: Deploy to Dev
    needs: [Build]
    runs-on: self-hosted
    environment: 
      name: Dev
    steps:
      - name: Deploy in dev
        run: cd /usr/local/bin/ && ./oc login $OC_SERVER -u $oc_USERNAME -p $oc_PASSWORD &&  ./oc project cp4i && ./oc apply -f  /home/bandaru/Videos/manoj/devops-dev.yaml 
    
  DeployStaging:
    name: Deploy to uat 
    needs: [Build]
    runs-on: self-hosted
    environment: 
      name: uat
    steps:
      - name: Deploy in uat
        run: cd /usr/local/bin/ && ./oc login $OC_SERVER -u $oc_USERNAME -p $oc_PASSWORD &&  ./oc project cp4i&&./oc apply -f  /home/bandaru/Videos/manoj/devops-uat.yaml 
            
  DeployProd:
    name: Deploy to prod 
    needs: [DeployStaging]
    runs-on: self-hosted
    environment: 
      name: prod
    steps:
      - name: Deploy in prod
        run: cd /usr/local/bin/ && ./oc login $OC_SERVER -u $oc_USERNAME -p $oc_PASSWORD &&  ./oc project cp4i && ./oc apply -f  /home/bandaru/Videos/manoj/devops-prod.yaml 
    
