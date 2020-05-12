# Deploying NVIDIA GPU Operator to OpenShift

## Prerequisites

OpenShift cluster with GPU-enabled nodes:

* [Amazon EC2 G4 Instances](https://aws.amazon.com/ec2/instance-types/g4/)
* [Amazon EC2 P3 Instances](https://aws.amazon.com/ec2/instance-types/p3/)

## Deploying Node Feature Discovery Operator

Deploy NFD operator using the command:

```
$ oc apply --kustomize nfd-operator/base
```

Verify that the NFD operator was deployed successfully:

```
$ oc get csv --namespace openshift-operators
NAME                     DISPLAY                  VERSION   REPLACES   PHASE
nfd.4.4.0-202004261927   Node Feature Discovery   4.4.0                Succeeded
```
Create an NFD master server instance:

```
$ oc apply --kustomize nfd-instance/base
```

Verify that the NFD pods are running on each of your cluster node:

```
$ c get ds --namespace openshift-nfd
NAME         DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR                     AGE
nfd-master   3         3         3       3            3           node-role.kubernetes.io/master=   3m7s
nfd-worker   6         6         6       6            6           node-role.kubernetes.io/worker=   3m7s
```

## References

* [Creating a GPU-enabled node with OpenShift 4.2 in Amazon EC2](https://www.openshift.com/blog/creating-a-gpu-enabled-node-with-openshift-4-2-in-amazon-ec2)
* [Simplifying deployments of accelerated AI workloads on Red Hat OpenShift with NVIDIA GPU Operator](https://www.openshift.com/blog/simplifying-deployments-of-accelerated-ai-workloads-on-red-hat-openshift-with-nvidia-gpu-operator)
* [How to install the NVIDIA GPU Operator with OpenShift](https://access.redhat.com/solutions/4908611)
