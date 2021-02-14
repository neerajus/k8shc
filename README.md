This repository contains a CLI tool 'k8shc' which can be run to quickly find health of your Kubernetes cluster and applications deployed on it.

Usage:

$  ./k8shc --help
CLI tool to get healthcheck of a Kubernetes cluster and applications running on it
Usage: k8shc [--cluster|app|help]
options:

cluster     Cluster Health Check
app         Applications Health Check
help        Print this Help

$  ./k8shc --cluster help
Usage: k8shc --cluster|-c  [verbose|help]

Cluster     Cluster Health Check
verbose     Cluster Health Verbose
help        Print this Help

Note:        not compatible with --app/-a

$  ./k8shc --app help
Usage: k8shc --app|-a  [-name appname]|[-namespace namespacename]|help]
Application health options:

name      Health of single Application
namespace Health of Application in a single namespace
help      Print this Help

Note:     not compatible with --cluster/-c


Notes: 

1. The healthceck tool CLI can be run from outside the cluster
2.  Kubernetes applications can mean different things, but in this tool I equate them to K8s deployments. I know that an application can be installed in other ways like pods or statefulsets, but deployments are the most common way of installing K8s applications.
3. An application or a deployment is considered healthy if number of ready pods are equal of the desired number of pods defined in its replicaset. It is assumed that the pods are configured with proper readiness or liveliness probes as Kubernetes cluster rely on them heavily to find the health of pods.
4. The applications can be internal or exposed externally using services, ingress. So I cannot assume that the service will be accessible from outside the cluster and if attached network poilicies allow such access. So tool does not make any direct network connection to applications. 
5. Except of the requirement listed below, the tool is a self contained bash script. It should with bash version 3.2.57 or later. 



Requirements for the tools:

1. curl should be installed ( On Ubuntu: sudo apt-get update; sudo apt-get install curl)
2. kubectl CLI utilities is installed and configured with  default context of target Kubernetes cluster and a user with appropriate access. I thought about not kubectl , but it would have required a complex SSL certificate setup before using the tool. 
See below reference links on setting up kubectl , kubeconfig, and users. 

https://kubernetes.io/docs/tasks/tools/install-kubectl/
https://kubernetes.io/docs/concepts/configuration/organize-cluster-access-kubeconfig/
https://kubernetes.io/docs/concepts/cluster-administration/certificates/

                                                                                                      
