```
kubectl apply -f - <<EOF
apiVersion: v1
data:
  username: YWRtaW4=
  password: MWYyZDFlMmU2N2Rm
kind: Secret
metadata:
  name: mysecret
  namespace: default
type: Opaque
EOF
```
```
kubectl apply -f -<<EOF
apiVersion: v1
kind: Pod
metadata:
  name: mypod
spec:
  containers:
  - name: mypod
    image: redis
    volumeMounts:
    - name: foo
      mountPath: "/etc/foo"
      readOnly: true
  volumes:
  - name: foo
    secret:
      secretName: mysecret
      optional: false # default setting; "mysecret" must exist
EOF
```
```
$ kubectl exec -it mypod -- cat /etc/foo/password
1f2d1e2e67df

$ kubectl exec -it mypod -- cat /etc/foo/username
admin
```
