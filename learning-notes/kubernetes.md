# Kubernetes Cheat Sheet

## Key Concepts

* **Pod** = Container + Layer to abstract the underlying container technology. Each pod has its own ip address
* **Service** is a static IP address to a pod and acts as load balancer for replicated pods
* All pod have a service. Lifetime of pod and service is not related
* **Ingress** is an "external service" which routes requests to services
* **ConfigMap** is an external configuration of the application, e.g. DB_URL
* **Secret** like ConfigMap, base64 encoded
* **Volume** attaches a physical storage to a pod
* **Deployment** is a blueprint for a pod. You can specify the number of replicas of a pod. Consider the template section as the blueprint for the pods
* Deployment, Spec for the deployment
  * Replicaset
    * Pod, Spec for the pod
* **StatefulSet** is a the deployment equivalent for stateful apps (databases). Ensures that database reads/writes are synchronized to avoid data inconsistencies
* **Worker** node consists of 3 processes
  * Container runtime
  * Kubelet handles the pods
  * Kube Proxy forwards the processes
* **Control Plane** node consists of 4 processes
  * **ApiServer** is a cluster gateway and a gatekeeper to the cluster
  * **Scheduler** determines where to place the pods (Scheduler -> asks Kubelet to schedule)
  * **Controller Manager** detects state changes like pod crashes
  * **Etcd** is a key value store. It is the cluster brain, provides information for the scheduler about the availability of resources

## kubectl

```sh
kubectl create deployment nginx-depl --image=nginx
kubectl edit deployment >deployment<
kubectl logs >pod<
kubectl exec -it >pod< — /bin/bash
kubectl apply/delete -f >file<
kubectl get pod -o wide
kubectl create namespace my-namespace
```

## Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mongodb-deployment
  labels:
    app: mongodb
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mongodb
  template:
    metadata:
      labels:
        app: mongodb
    spec:
      containers:
        - name: mongodb
          image: mongo
          ports:
            - containerPort: 27017
          env:
            - name: MONGO_INITDB_ROOT_USERNAME
              valueFrom:
                secretKeyRef:
                  name: mongodb-secret
                  key: mongo-root-username
            - name: MONGO_INITDB_ROOT_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: mongodb-secret
                  key: mongo-root-password
--- # separates yaml files
apiVersion: v1
kind: Service
metadata:
  name: mongodb-service
spec:
  selector:
    app: mongodb
  ports:
    - protocol: TCP
      port: 27017       # exposed service port for all pods
      targetPort: 27017 # matches containerPort
---
apiVersion: v1
kind: Secret
metadata:
    name: mongodb-secret
type: Opaque
data:
    mongo-root-username: dXNlcm5hbWU= # echo -n 'username' | base64
    mongo-root-password: cGFzc3dvcmQ= # echo -n 'password' | base64
```

Each config has three parts:

  1. Metadata
  2. Specification
  3. An automatically generated status comparing desired and actual state (self healing feature provided by etcd)

Service's selector (`app: nginx`) and the deployment's label `app:nginx` define which pods are registered to the service.

## Ingress & External Services

* Service's `targetPort` has to be equal to the pod's `containerPort`
* LoadBalacner is an external service and opens up `nodePort`
* LoadBalancer is only used **without** Ingress, because Ingress has rules to map an external url to an internal service
* Ingress Controller must be installed in the cluster separately
* This requires a **proxy server** with a public ip address to redirect requests to the ingress controller
* For minikube:

```sh
minikube addons enable ingress
minikube service mongo-express-service
```

## Namespaces

* Namespaces are virtual cluster inside a cluster
* Standard Namespaces
  * `kube-system`: processes kubectl
  * `kube-public`: contains public information, `kubectl cluster info`
  * `kube-node-lease`: heartbeats of nodes
  * `default`

### Grouping

* Logical grouping: Database Namespace, Monitoring Namespace, Nginx Ingress
* Staging and Development Grouping
* Blue/Green Deployment, if they use the same resources
  * Production Blue (is active)
  * Production Green (will be active)
* One Namespace per team

### Limitations

* Cannot use configmaps/secrets between namespaces
* Volume/node cannot be namespaces
* `kubens`/`kubectx` allows to select the default namespace in the shell

## Helm Chart

* Package Manager for Kubernetes
* [ArtifactHub](https://artifacthub.io): Can bundle a complete tech stack
* `values.yaml` contains configuration values
* `chart.yaml` contains metadata
* `charts/` folder contains chart dependencies
* `templates/` contains the actual charts


## Storage

### Requirements

1. Storage does not depend on pod lifecycle
2. Storage must be available on all nodes
3. Storage need to survive if cluster crashes

### Persistent Volumes

* **Persistent Volumes** are a cluster resource like memory, they must exist before pods exist
* Local storage violates requirement 2 and 3, for **database persistency, it is best to create a remote storage**
* Applications do not directly use PV, but have to claim to use volumes: **Persistent Volume Claims**
* PV are not namespaced
* PVC are namespaced
* **Storage Classes** create persistent volumes in the background via a **provisioner**
* Storage Classes are called from the PVC

## Statefulset

* Replicas maintain a sticky identity for each pod
  * Pods are name (Statefulsetname)-(ordinal), master = 0
  * Pods have fixed DNS Name
* Pods are created from the same spec but are not interchangeable
* Only the master pod is allowed to write to a DB, the other workers are only allowed to read
* Pods need to sync the data all the time
* Due to the sticky identity remote storage should be used
