# kubernetes-hello-app

Kubernetes Hello App taken from https://github.com/GoogleCloudPlatform/kubernetes-engine-samples/tree/master/hello-app

## Tools

- kustomize `>= 3.6`

## Create the app

- Create resources:

```bash
kustomize build . | kubectl apply -f -
```

- Add the following line to the bottom of the /etc/hosts file:

```bash
<MINIKUBE_IP> hello-world.info
```

Where `<MINIKUBE_IP>` must be replace with output of `minikube ip`.

- Verify that the Ingress controller is directing traffic:

```bash
curl hello-world.info
```

## Update app

To update the app you need to change the `image` field of the `hello-deployment` from `image: gcr.io/google-samples/hello-app:1.0` to `image: gcr.io/google-samples/hello-app:2.0`.

This can be achieved in various ways. The simplest way is:

```bash
kubectl set image -n hello deployment/hello-app hello-app=gcr.io/google-samples/hello-app:2.0
```

Alternatively you can edit the deployment and change the version via:

```bash
kubectl edit deployments.apps -n hello hello-app
```

## Credits

- https://github.com/GoogleCloudPlatform/kubernetes-engine-samples/tree/master/hello-app
- https://kubernetes.io/docs/tasks/access-application-cluster/ingress-minikube/
