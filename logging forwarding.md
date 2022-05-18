apiVersion: "logging.openshift.io/v1"
kind: ClusterLogForwarder
metadata:
  name: instance
  namespace: openshift-logging
spec:
  outputs:
   - name: elasticsearch-insecure
     type: "elasticsearch"
     url: http://192.168.3.181:9200
   - name: kafka-app
     type: "kafka"
     url: http://192.168.3.181:9093/devopsopenshift
  inputs:
   - name: my-app-logs
     application:
        namespaces:
        - manoj
  pipelines:
   - name: audit-logs
     inputRefs:
      - audit
      - application
      - infra
     outputRefs:
      - elasticsearch-insecure
      - default
