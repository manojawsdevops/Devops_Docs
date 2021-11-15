Secret command:-Oc create secret docker-registry regcred --docker-server=https://hub.docker.com/ --docker-username=manojreddyeidiko --docker-password=Ashwanth@8801
policy command:-oc project manoj
oc adm policy add-scc-to-group anyuid system:serviceaccounts:manoj


oc new-app --docker-image=manojreddyeidiko/log4j:latest -e LICENSE=accept
oc expose service log4j -l name=dockerlog --port=7800

