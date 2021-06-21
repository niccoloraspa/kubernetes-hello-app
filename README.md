# kubernetes-hello-app

Kubernetes Hello App taken from https://github.com/GoogleCloudPlatform/kubernetes-engine-samples/tree/master/hello-app

## Tools

- kustomize `>= 3.6`

## Deploy the app

Create resources:

```bash
kustomize build . | kubectl apply -f -
```

### Interact with the app (Minikube)

Add the following line to the bottom of the `/etc/hosts` file:

```bash
curl -H "Host: hello-world.info" $(minikube ip)
```

## Update app

To update the app, change the `image` field of the `hello-deployment`:

- from `image: gcr.io/google-samples/hello-app:1.0` 
- to `image: gcr.io/google-samples/hello-app:2.0`.

```bash
kubectl set image -n hello deployment/hello-app hello-app=gcr.io/google-samples/hello-app:2.0
```

Alternatively you can edit the deployment and change the version via:

```bash
kubectl edit deployments.apps -n hello hello-app
```

## Credits

- https://github.com/GoogleCloudPlatform/kubernetes-engine-samples/tree/master/hello-app
