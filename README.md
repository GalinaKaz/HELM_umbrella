# Helm_Umbrella
**Description :** promethues grafana redis and redis exporter

Configuration file Chart.yaml contains all the dependencies :
1. promethues+grafana : kube-prometheus-stack from  prometheus-community repository
2. redis :  from bitnami repository 
3. redis-exporter: prometheus-redis-exporter from prometheus-community repository

Configuration file values.yaml is for some values that will be modified from the default installation 
for example number of replicas for redis database (default is 3).
For exporter of redis its CRITICAL to change the parameter of release, before running the installation !!!!

**Prerequires:**

1. Kubernetes cluster installed and accessible
2. Helm installed

**STEP 1 :**

Run build command, in order HELM will build and download all dependencies 

$ helm dependency build  <THE_CHART_DIRECTORY_NAME>

in this case:

$ helm dependency build Helm_Umbrella

**STEP 2:**

Change the release parameter in section related to redis exporter to match the name that will be applied later by HELM as RELEASE_NAME


**Explanations:**

the serviceMonitor.labels.release is set as "example1" at values.yaml, this values should be changed if you plan different name as helm release as will appear in step3

**STEP3:**

$ helm install <RELEASE_NAME> <CHART_DIRECTORY> 

in this case :

$ helm install example1 Helm_Umbrella

this command will create example1 release that can be see with "helm list" command 

**CRITICAL**   :  the RELEASE_NAME must match the serviceMonitor.labels.release for redis exporter section, in order to make sure redis will be monitored by prometheus.

