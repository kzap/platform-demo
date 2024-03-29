# Local Internal Developer Platform using Kratix

This sets up a local Kubernetes cluster using KinD (Kubernetes in Docker) and installs ArgoCD and uses it to sync the following applications onto the cluster:

### Core Services:
- argocd - deployment tool
- cert-manager - certificates
- ingress-nginx - ingress reverse proxy
- kratix-platform
  - gitea
    - metallb - for exposing git server to 
- kratix worker examples

### Applications:
- emojivoto sample application
- sample application that requests Kratix promises

The goal is to have a Platform and a Worker Kubernetes cluster running and the source of truth being this GitHub repository. Kratix will be used as a platform to deploy custom resources onto the worker cluster.

> This is based on the [Kratix Quickstart](https://kratix.io/docs/workshop/installing-kratix) tutorial.

## Getting Started

- Make sure you have KinD installed:

    ```sh
    brew install kind
    ```

- Create the KinD clusters from the config:

    ```sh
    kind create cluster --config ./kind/cluster-platform.yaml
    kind create cluster --config ./kind/cluster-worker.yaml
    ```

- Install ArgoCD using `kustomize` so it can fetch all the other applications (Run it twice because CRDs are installed the first time)

    ```sh
    kubectl --context kind-platform apply -k ./gitops-repo/argocd/platform
    kubectl --context kind-platform apply -k ./gitops-repo/argocd/platform
    kubectl --context kind-worker apply -k ./gitops-repo/argocd/worker
    kubectl --context kind-worker apply -k ./gitops-repo/argocd/worker
    ```

- You can observe the Kratix Platform commiting to the local Git Server by opening the URL: https://0.0.0.0:8333/
    
    > Login with the credentials here: https://github.com/syntasso/kratix/blob/e40901e658772057c0c4d6526cbe58cd8951e91a/hack/platform/gitea-install.yaml#L846-L849

    - 