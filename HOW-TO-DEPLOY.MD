# How to Deploy

## Introduction

Welcome to the deployment guide for [OS2-PROJECTNAME]. This document will walk you through the process of deploying pre-built containers, whether you're setting up a development environment or deploying to a production cluster.

## Prerequisites

Before proceeding with the deployment, please ensure you have the following prerequisites met:

- Docker or Podman installed for local container management.
- Access to the [OS2-PROJECTNAME] container images.
- For production deployments:
  - Access to the Kubernetes cluster where you will deploy the application.
  - **For Helm users**: Helm package manager installed. If you do not have Helm installed, please refer to the official Helm installation guide.

## 💻 Development

To set up a containerized development and test environment you can use the `docker run` or `podman run` to pull the containerimage and run the container.

### Docker
```shell
docker run -d -p {CONTAINERPORT:HOSTPORT} --name {CONTAINER_NAME} {IMAGE_NAME}:{TAG}
```
[Official documentation for `docker run`](https://docs.docker.com/reference/cli/docker/container/run/)

### Podman
```shell
podman run -d -p {HOSTPORT}:{CONTAINERPORT} --name {CONTAINER_NAME} {IMAGE_NAME}:{TAG}
```
[Official documentation for `podman run`](https://docs.podman.io/en/latest/markdown/podman-run.1.html)


## 🚢 Production

To deploy [OS"-PROJECTNAME] to production use the supplied templates in the deployment-repository here: {DEPLOYMENTREPO-URL}

### 🌐 Manual push deployment with Helm

Manual push deployments involve a developer or an operator directly deploying changes to a Kubernetes cluster using tools like the Helm package manager. 

To manually push a deployment to a Kubernetes cluster with the chart from the {DEPLOYMENTREPO-URL}, you can use the `helm install` command.

Here's a basic example:

```shell
helm install {RELEASE_NAME} {CHART_PATH} --values {VALUES_FILE}
```
[Official documentation for `helm install`](https://helm.sh/docs/helm/helm_install/#helm)

For detailed information on the Helm chart structure and syntax, you can refer to the [Helm Charts documentation](https://helm.sh/docs/topics/charts/).

### Automatic push deployment with GitOps tools

