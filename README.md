# MyK8s


`kubectl create -f hybrid-declarative.yml`

to edit directly in control plane

`kubectl edit deployments first-deployment`

describe deployment

`kubectl describe deployment first-deployment`

scaling 
    
`kubectl scale deployment --replicas=3 first-deployment`


labeling Nodes
 
```kubectl label nodes docker-for-desktop env=dev
kubectl get nodes --show-labels
kubectl get pods --show-labels
kubectl get pods -o=wide
kubectl get pods -o=json
```
init containers

```

spec:
  containers:
  - name: nginx
    image: nginx
    ports:
    - containerPort: 80
    volumeMounts:
    - name: workdir
      mountPath: /usr/share/nginx/html
  # These containers are run during pod initialization
  initContainers:
  - name: install
    image: busybox
    command:
    - wget
    - "-O"
    - "/work-dir/index.html"
    - http://kubernetes.io
    volumeMounts:
    - name: workdir
      mountPath: "/work-dir"
  dnsPolicy: Default
  volumes:
  - name: workdir
    emptyDir: {}
```
