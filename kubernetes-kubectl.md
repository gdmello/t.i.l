# JSONPath
Kubectl + JSONPath [support](https://kubernetes.io/docs/reference/kubectl/jsonpath/).
##Examples-
* retrieve a key with a dot in a map-

        $ kubectl -n <my-namespace> get secrets prometheus-mypod-prometheus -o "jsonpath={.data['prometheus\.yaml']}"
        Z2xvYmFsOgogIGV2YWx1YXRpb25faW50ZXJ2YWw6IDMwcwogIHNjcmFwZV9pbnRlcnZhbDogMzBzCiAgZXh0ZXJuYWxfbGFiZWxzOgogI

* Retrieve Alertmanager config

        $ kubectl -n sys-monitoring get secrets alertmanager-prometheus-operator-alertmanager -o json | jq -c '.data["alertmanager.yaml"]' | sed 's/\"//g' |  base64 -d

# Dry Run (Auto Generate YAML)

```
$ kc create deployment --dry-run=client --image=nginx test -o yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: test
  name: test
spec:
  replicas: 1
  selector:
    matchLabels:
      app: test
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: test
    spec:
      containers:
      - image: nginx
        name: nginx
        resources: {}
status: {}
```
[How to create and change the Kubernetes yaml using dry-run and edit](https://foxutech.medium.com/how-to-create-and-change-the-kubernetes-yaml-using-dry-run-and-edit-5975d77e8df2)

[Kubectl API Docs](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands)
