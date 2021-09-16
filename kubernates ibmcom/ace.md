apiVersion: apps/v1
kind: Deployment
metadata:
  name: manoj
  labels:
    app: ace
spec:
  replicas: 3
  selector:
    matchLabels:
      app: ace
  template:
    metadata:
      labels:
        app: ace
    spec:
      containers:
      - name: manoj
        image: ibmcom/ace    
        command: [ "/bin/bash", "-ce", "tail -f /dev/null" ]
