## Elasticsearch

These manifests install Elasticsearch itself as a stateless set  of two pods . A Service is created in front of the StatefulSet pods to load balance them.
Elasticsearch is also configured to run under the service account elasticsearch-logging, which gets bound to the role of the same name in order for it to have the right permissions. 

* es-statefulset.yaml
* es-service.yaml

## Fluentd

Fluentd is installed as a DaemonSet, which means that a corresponding pod will run on every Kubernetes worker node in order to collect its logs (and send them to Elasticsearch). Furthermore, the pods run as the service account fluentd-es which is bound to the cluster role with the same name in order to have the necessary permissions.

* fluentd-es-configmap.yaml
* fluentd-es-ds.yaml

## Kibana

Installs a Deployment, which ensures that one pod is always running, and a Service in front of it (which is capable of load balancing in case there should be several pods in parallel).

* kibana-deployment.yaml
* kibana-service.yaml



## Additional info##

Istio injection is disabled for this specific services , so nodeport expose will be used for accessing kibana.
Stateless-set will be changed to stategull set 