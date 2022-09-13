# Deploying a Python microservice to Tanzu Application Platform

This example builds a `helloworld-python` sample app using Tanzu Application Platform,
and deploys it to a Tanzu Kubernetes Grid cluster.

You can either have TAP do the entire CI/CD pipeline, or you can build a container image locally, and have TAP deploy it.

## Prerequisites

- A [Tanzu Kubernetes Grid](https://tanzu.vmware.com/kubernetes-grid) cluster<br />
  Configure the correct context using a command of the form:<br />
  ``kubectl config use-context <MY-CONTEXT>``
- [Tanzu Application Platform](https://tanzu.vmware.com/application-platform)
- (Optional, if building an image locally): [Docker](https://www.docker.com) installed and running on your local machine,
  and a [Docker Hub](https://hub.docker.com/) account configured.
- Either edit the makefile, or [over-ride variable values on the Make command line](https://www.gnu.org/software/make/manual/html_node/Overriding.html), so as to set two required variables:
  - ``NAMESPACE`` - the Kubernetes namespace into which the app will be deployed;<br />and
  - ``DOCKER_HUB_USERNAME`` - your username on Docker Hub.

## Building and deploying from source code using TAP

1. Execute:<br />
   ``make source``

## Building an image locally, then deploying it using TAP

1. Execute:<br />
   ``make image``

## Verification

1. Use this command to find the domain URL for your service:<br />
  ``make get``

1. Now you can make a request to your app and see the result.
   Either open the URL displayed above in your web browser,
   or in ``curl`` using a command of the form:<br />
   ``curl --verbose --fail <URL>``

## Removing

To remove the sample app from your cluster, execute:<br />
    ``make delete``

## Adding custom accelerator

You can add an accelerator to your deployment of Tanzu Application Platform that creates (optionally customised) instances of this application.
To do this:
1. Check out this git repository, for example:<br />
   ``git clone https://github.com/balnbibarbi/helloworld-python.git``
1. Enter the repository directory, for example:<br />
   ``cd helloworld-python``
1. Log in to the Kubernetes cluster hosting Tanzu Application Platform, for example:<br />
   ``kubectl config use-context my-k8s-tap``
1. Define the accelerator:<br />
   ``kubectl apply -n accelerator-system -f tap-accelerator.yaml``
