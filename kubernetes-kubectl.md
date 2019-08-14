# JSONPath
Kubectl + JSONPath [support](https://kubernetes.io/docs/reference/kubectl/jsonpath/).
##Examples-
* retrieve a key with a dot in a map-

        $ kubectl -n <my-namespace> get secrets prometheus-mypod-prometheus -o "jsonpath={.data['prometheus\.yaml']}"
        Z2xvYmFsOgogIGV2YWx1YXRpb25faW50ZXJ2YWw6IDMwcwogIHNjcmFwZV9pbnRlcnZhbDogMzBzCiAgZXh0ZXJuYWxfbGFiZWxzOgogI

* Retrieve Alertmanager config

        $ kubectl -n sys-monitoring get secrets alertmanager-prometheus-operator-alertmanager -o json | jq -c '.data["alertmanager.yaml"]' | sed 's/\"//g' |  base64 -d

