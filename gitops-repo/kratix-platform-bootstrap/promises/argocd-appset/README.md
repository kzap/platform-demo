# Demo: ArgoCD AppSet

This Promise provides an ArgoCD Appset.

- name: service name, if left empty will use the object name

To install:

```
kubectl create -f https://raw.githubusercontent.com/kzap/platform-demo/main/gitops-repo/kratix-platform-bootstrap/promises/argocd-appset-promise/promise.yaml
```

Make sure you have ArgoCD installed on your worker clusters

To make a resource request:

```
kubectl apply -f https://raw.githubusercontent.com/kzap/platform-demo/main/gitops-repo/kratix-platform-bootstrap/promises/argocd-appset-promise/resource-request.yaml
```
<!--
This resource request deploys the Kratix [sample Golang app](https://github.com/syntasso/sample-golang-app).

To test the sample app once it is successfully deployed, port forward with command below and access at `http://todo.default.local.gd:8081`:

```
kubectl --context kind-worker --namespace knative-serving port-forward svc/kourier 8081:80
```
-->

## Development

For development see [README.md](./internal/README.md)

<!--
## Questions? Feedback?

We are always looking for ways to improve Kratix and the Marketplace. If you run into issues or have ideas for us, please let us know. Feel free to [open an issue](https://github.com/syntasso/kratix-marketplace/issues/new/choose) or [put time on our calendar](https://www.syntasso.io/contact-us). We'd love to hear from you.
-->
