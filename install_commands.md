
#### Patch hive

oc patch hiveconfig hive --type merge -p '{"spec":{"targetNamespace":"hive","logLevel":"debug","featureGates":{"custom":{"enabled":["AlphaAgentInstallStrategy"]},"featureSet":"Custom"}}}'

### HUB Cluster basic elements creation



#### create imageset
oc create -f clusterimageset_v4.9.18.xml

### check imgset
oc get imgset | grep openshift-v4.9.18


#### deploy config map (NOT USED IN PROD)



update the sha256 to latest 

oc create -f assistedserviceconfig.yml

#### check cm
oc get cm | grep assisted-service-config


#### Deploy AgentServiceConfig - this is the Assisted Service  that handles Spoke cluster deployments


#### deploy the pull secret (copy from openshift-config to ns to open-cluster-management)


oc get secret pull-secret --namespace=openshift-config -o yaml | sed 's/namespace: .*/namespace: open-cluster-management/' | oc apply -f -





# USEFUL

oc get event --sort-by=.metadata.creationTimestamp

oc get  subscriptions.apps.open-cluster-management.io

in case of issues we can try see logs in **infrastructure-operator**
