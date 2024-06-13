# How to Deploy

## Introduction

Welcome to the deployment guide for [OS2-PROJECTNAME]. This document will walk you through the process of deploying pre-built containers, whether you're setting up a development environment or deploying to a production cluster.

## 💻 Development
To set up a containerized development and test environment on a local computer or in a hosted developer enviroment like GitHub codespaces, you can use the `docker run` or `podman run` to pull the containerimage and run the container.

### Prerequisites

- Docker or Podman installed for local container management.
- Access to the [OS2-PROJECTNAME] container images.


### 🗳️ Docker example
```shell
docker run -d -p {CONTAINERPORT:HOSTPORT} --name {CONTAINER_NAME} {IMAGE_NAME}:{TAG}
```
[Official documentation for `docker run`](https://docs.docker.com/reference/cli/docker/container/run/)

### 🐭 Podman example
```shell
podman run -d -p {HOSTPORT}:{CONTAINERPORT} --name {CONTAINER_NAME} {IMAGE_NAME}:{TAG}
```
[Official documentation for `podman run`](https://docs.podman.io/en/latest/markdown/podman-run.1.html)


## 🚢 Production

### Deployment on a single host
For less demanding production environments on a single VM or bare metal host, you can use tools like Ansible, Chef, or Puppet to deploy the container.

### Prerequisites

- Ansible installed for server configuration management.
- Access to the [OS2-PROJECTNAME] container images in a registry.
- A user account on the remote host with sufficient privileges to execute Ansible commands.
- SSH keys for passwordless login between your local machine and the remote host. This involves generating an SSH key pair and adding the public key to the `authorized_keys` file on the remote host.
- Properly configured environment variables and volumes for production use.

### 🅰️ Ansible Example
Use the following command to run `ansible-pull` from your local machine on the remote host via SSH:

```shell
ssh remote_user@remote_host "ansible-pull -U https://github.com/{USERNAME}/{REPOSITORY}.git \\
             -e 'container_port={CONTAINERPORT}' \ 
             -e 'host_port={HOSTPORT}' \          
             -e 'container_name={CONTAINER_NAME}' \ 
             -e 'image_name={IMAGE_NAME}' \ 
             -e 'tag={TAG}'"
```

---

### 🌐 Cluster Deployment
For more demanding production environments that require scalability, fault tolerance, observability and high availability container orchestration tools like [Kubernetes](https://kubernetes.io/), [Nomad](https://www.hashicorp.com/products/nomad), [OpenShift](https://www.openshift.com/) is recommended alongside [GitOps](https://opengitops.dev/) tools like [ArgoCD](https://argoproj.github.io/argo-cd/), [Flux](https://fluxcd.io/) or [Fleet](ttps://rancher.com/docs/rancher/v2.x/en/deploy-across-clusters/fleet/
) to ensure a streamlined and robust deployment process.

### 📦 Kubernetes example with Rancher & Fleet

### Prerequisites

- A **Rancher-managed Kubernetes cluster** using **RKE2 (RKE Government)**, designed for security and compliance within the Government sector, with FIPS 140-2 compliance and configurations for passing CIS Kubernetes Benchmarks.
- **Fleet GitOps controller** for automated deployments.
- **Access to the deployment repository** containing the [OS2-PROJECTNAME] Helm chart.

#### 🛠️ Deployment Steps

1. **Rancher Setup**: Configure your RKE2 Kubernetes cluster with Rancher for an intuitive management experience.
2. **Fleet Configuration**: Integrate Fleet in Rancher for GitOps deployments, tracking changes to the [OS2-PROJECTNAME] Helm chart.
3. **Helm Chart**: Ensure the Helm chart is updated in the repository with all configurations.
4. **Deployment Trigger**: Updates to the Helm chart in the Git repository will prompt Fleet to deploy within the Rancher-managed cluster.

This streamlined process utilizes Kubernetes' orchestration, Rancher's management, and Fleet's continuous deployment for a secure, government-focused deployment pipeline.
