# Local Internal Developer Platform using Kratix

This sets up a local Kubernetes cluster using KinD (Kubernetes in Docker) and installs ArgoCD and uses it to sync the following applications onto the cluster:

- argocd
- ingress-nginx
- cert-manager

It then allows you to create AWS resources using Crossplane such as an entire EKS cluster as shown below.

## Getting Started

- Make sure you have KinD installed:

    ```sh
    brew install kind
    ```

- Create the KinD cluster from the config:

    ```sh
    kind create cluster --config ./kind/platform-cluster.yaml
    ```

- Install ArgoCD using `kustomize` so it can fetch all the other applications (Run it twice because CRDs are not installed the first time)

    ```sh
    kubectl --context kind-platform apply -k ./gitops-repo/argocd
    kubectl --context kind-platform apply -k ./gitops-repo/argocd
    ```
