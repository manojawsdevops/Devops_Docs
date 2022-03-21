Secret command:-Oc create secret docker-registry regcred --docker-server=https://hub.docker.com/ --docker-username=manojreddyeidiko --docker-password=Ashwanth@8801
policy command:-oc project manoj
oc adm policy add-scc-to-group anyuid system:serviceaccounts:manoj


oc new-app --docker-image=manojreddyeidiko/log4j:latest -e LICENSE=accept
oc expose service log4j -l name=dockerlog --port=7800



oc patch configs.imageregistry.operator.openshift.io/cluster --type merge -p '{"spec":{"defaultRoute":true}}'
oc patch configs.imageregistry.operator.openshift.io cluster --type merge --patch '{"spec":{"managementState":"Managed"}}'
oc patch configs.imageregistry.operator.openshift.io cluster --type merge --patch '{"spec":{"storage":{"emptyDir":{}}}}'
docker login -u kubeadmin -p $(oc whoami -t) default-route-openshift-image-registry.apps.ocp4.eidikointernal.com




