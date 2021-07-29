# Autoscaling-K8
The Horizontal Pod Autoscaler automatically scales the number of Pods in a replication controller, deployment, replica set or stateful set based on observed CPU utilization or with custom metrics support.

Simple example to demonstrate the application of autoscaling-

Steps followed:

*As Root*
```

1. Create the Deployment, service and horizontal autoscaler.
$ kubectl apply -f hpa.yaml
$ kubectl apply -f hpa_service.yaml
$ kubectl apply -f autoscaler.yaml

2. Increase the load on pod on Master node with a separate terminal using Busybox.
$ kubectl run -i --tty load-generator --rm --image busybox --restart Never -- /bin/sh -c "while sleep 0.01; do wget -q -O- http://php-apache:7000; done"

3. Monitor the autoscaler creating replicas once the load threshold is more than 50%
$ watch kubectl get hpa

4. Stop the load triggering on Pod from the separate terminal and watch the autoscale- down feature. PS: this takes around 5 minutes after the load has dropped below 50%.
$ CNTRL+ Z


```
*As Root*
