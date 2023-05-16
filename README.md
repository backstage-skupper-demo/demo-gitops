# Backstage Skupper Demo
This is a repo to configure and use the demo

## Setup
Deploy this root application into openshift gitops
```
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: backstage-demo
  namespace: openshift-gitops
spec:
  destination:
    namespace: openshift-gitops
    server: 'https://kubernetes.default.svc'
  project: default
  source:
    path: .
    repoURL: 'https://github.com/backstage-skupper-demo/demo-gitops.git'
    targetRevision: HEAD
```

Create a secret for your github personal access token

Follow  https://backstage.io/docs/getting-started/configuration#setting-up-a-github-integration for the GITHUB_TOKEN value
Create a new OAuth application here https://github.com/settings/applications/new and specify the url to match your ingress host address.  The output of this goes to auth_github_client_id and secret.
```
kind: Secret
apiVersion: v1
metadata:
  name: github-pat
  namespace: backstage
stringData:
  GITHUB_TOKEN: ''
  AUTH_GITHUB_CLIENT_ID: ''
  AUTH_GITHUB_CLIENT_SECRET: ''
type: Opaque

```