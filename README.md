# argocd-sync GitHub Action

This GitHub Action uses ArgoCD to synchronize your Kubernetes deployments.

## Usage

Add the following step to your GitHub Actions workflow file:

```yaml
- name: Sync ArgoCD Applications
  uses: tallmanbrew/argocd-sync@v1
  with:
      argocd-http-server: ${{ secrets.ARGOCD_HTTP_SERVER }}
      argocd-grpc-server: ${{ secrets.ARGOCD_GRPC_SERVER }}
      argocd-token: ${{ secrets.ARGO_TOKEN }}
      application: application-name
      restart-deployments: True
```

### Inputs
This action requires the following environment variables:

`argocd-http-server`: (Required) The http address of your ArgoCD server  
`argocd-grpc-server`: The grpc address of your ArgoCD server.  
`argocd-token`: (Required) ArgoCD API Token.  
`application`: (Required) Application name to sync.  
`restart-deployments`: (Required) True | False Restart the applications after sync to pickup new image.

### Outputs
This action does not have any outputs.

## Example
Here's an example of how to use this action in a workflow:

```yaml
name: Deploy with ArgoCD

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v4

    - name: Sync ArgoCD Applications
      uses: tallmanbrew/argocd-sync@v1
      with:
        argocd-http-server: ${{ secrets.ARGOCD_HTTP_SERVER }}
        argocd-grpc-server: ${{ secrets.ARGOCD_GRPC_SERVER }}
        argocd-token: ${{ secrets.ARGO_TOKEN }}
        application: application-name
        restart-deployments: True
```