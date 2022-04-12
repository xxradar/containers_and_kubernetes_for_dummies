```
kubectl apply -f - <<EOF
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: psn-reader
rules:
- apiGroups: [""]
  resources: ["pods", "services", "nodes"]
  verbs: ["get", "watch", "list"]
EOF
```
```
kubectl apply -f - <<EOF
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: read-psn-global
subjects:
- kind: ServiceAccount
  name: default #name is case sensitive
  namespace: default
roleRef:
  kind: ClusterRole
  name: psn-reader
  apiGroup: rbac.authorization.k8s.io
EOF
```

```
docker run --it --rm --image xxradar/hackon -- bash
KUBE_TOKEN=$(</var/run/secrets/kubernetes.io/serviceaccount/token)
KUBE_CA="/var/run/secrets/kubernetes.io/serviceaccount/ca.crt"
curl -kv   https://kubernetes/api/v1/
curl -kv   https://kubernetes/version
curl --cacert $KUBE_CA  https://kubernetes/api/v1/
curl --cacert $KUBE_CA -H "Authorization: Bearer $KUBE_TOKEN"  https://kubernetes/api/v1/
curl --cacert $KUBE_CA -H "Authorization: Bearer $KUBE_TOKEN"  https://kubernetes/apis/
curl --cacert $KUBE_CA -H "Authorization: Bearer $KUBE_TOKEN"  https://kubernetes/apis/crd.projectcalico.org/v1
curl --cacert $KUBE_CA -H "Authorization: Bearer $KUBE_TOKEN"  https://kubernetes/api/v1/namespaces/default/pods/demo/
```
