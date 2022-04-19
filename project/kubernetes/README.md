## Kubernetes Declarative Manifests 

Place the Kubernetes declarative manifests in this directory.

# Namespace

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: sandbox
```


# Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: techtrends
  name: techtrends
  namespace: sandbox
spec:
  replicas: 1
  selector:
    matchLabels:
      app: techtrends
  template:
    metadata:
      labels:
        app: techtrends
    spec:
      containers:
      - image: nat389/techtrends:latest
        name: techtrends
        ports:
        - containerPort: 3111
        resources: {}
        resources:
            requests:
                memory: "64Mi"
                cpu: "250m"
            limits:
                memory: "128Mi"
                cpu: "500m"
        livenessProbe:
            httpGet:
                path: /healthz
                port: 3111
            initialDelaySeconds: 10
            periodSeconds: 5
        readinessProbe:
            httpGet:
                path: /healthz
                port: 3111
            initialDelaySeconds: 10
            periodSeconds: 5
```

# Service

```yaml
apiVersion: v1
kind: Service
metadata:
  name: techtrends
  namespace: sandbox
spec:
  selector:
    app: techtrends
  ports:
    - protocol: 
      port: 4111
      targetPort: 3111
  type: ClusterIP
```