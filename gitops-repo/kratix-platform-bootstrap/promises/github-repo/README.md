# Demo: Ada Service

This Promise provides an Ada Service. This is a compound Promise that installs the following Promises:

- [Slack](https://github.com/syntasso/kratix-marketplace/tree/main/slack)

The following fields are configurable:

- repoName: Repository Name
- orgName: The GitHub Org where this will be created
- templateName: The GitHub repo template to clone

To install:

```
kubectl create -f https://raw.githubusercontent.com/kzap/platform-demo/main/gitops-repo/kratix-platform-bootstrap/promises/github-repo-promise/promise.yaml
```

Make sure you install the GitHub Access Token on the platform before making the resource request.

-  Create a GitHub Access Token following this guide: https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token

- Store the GitHub Access Token in an environment variable:

```sh
GITHUB_TOKEN=ghp_
```

- Create the Kubernetes secret where this webhook will be stored:

```sh
kubectl --namespace default create secret generic \
  github-repo-promise --from-literal=github_token=${GITHUB_TOKEN}
```

Make sure you install the Slack hook on the platform before making the resource request.

> (via the [Slack Promise](https://github.com/syntasso/kratix-marketplace/tree/main/slack) in the Marketplace) This promise uses a Slack hook to send messages to a channel. To provide access to this hook, create a secret in default namespace called slack-channel-hook with a .data.url field containing the hook. You can create it using the following command on the platform cluster (ensure you have SLACK_HOOK_URL env var exported):

-  Create a Slack Webhook following this guide: https://slack.com/help/articles/115005265063-Incoming-webhooks-for-Slack

- Store the Slack Webhook in an environment variable:

```sh
SLACK_HOOK_URL=https://hooks.slack.com/services/
```

- Create the Kubernetes secret where this webhook will be stored:

```sh
kubectl --namespace default create secret generic \
  slack-channel-hook --from-literal=url=${SLACK_HOOK_URL}
```

To make a resource request:

```
kubectl apply -f https://raw.githubusercontent.com/kzap/platform-demo/main/gitops-repo/kratix-platform-bootstrap/promises/github-repo-promise/resource-request.yaml
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
