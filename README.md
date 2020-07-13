# RBAC Playground
## Example
This repo provides an example of how to create a role, rolebinding and
serviceaccount. This is then used to show that the serviceaccount can only see
resources that its role has permissions to view

1. `kubectl create -f .`
1. To get the token for the serviceaccount run `kubectl get secretsmy-service-account-token-vl7fn -o jsonpath='{.data.token}' | base64 --decode> token`
1. To add this token to our kubeconfig run `kubectl config set-credentials sa-token --token="$(cat token)"`
1. Finally to set our current context to use this credential run `kubectl config set-context --current --user=sa-token`

You should now see that you are only able to list pods in the `dev` namespace and not the `prod`
`kubectl get pods -n=dev`
`kubectl get pods -n=prod`
