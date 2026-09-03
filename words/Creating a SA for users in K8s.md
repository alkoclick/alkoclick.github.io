Kinda cursed, you should only do this for temp work, but hey, it works:

```
apiVersion: v1
kind: Secret
metadata:
  name: ucro-secret
  annotations:
    kubernetes.io/service-account.name: ucro
type: kubernetes.io/service-account-token

apiVersion: v1
kind: ServiceAccount
metadata:
  name: ucro

apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: ucro
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: view
subjects:
  - kind: ServiceAccount
    name: ucro
    namespace: NAMESPACE
```

Then copy over an existing kubeconfig and run:
* `TOKEN=$(kubectl -n NAMESPACE get secret ucro-secret -o jsonpath='{.data.token}' | base64 -d -)`
* `k config set-credentials ucro --token "$TOKEN"`
* `export KUBECONFIG=KUBECONFIG` and you're good to go!
