# k8s-dbg-ymls

A collection of Kubernetes manifests to deploy a debugging pod with both Alpine and
Ubuntu containers. Images are from [here](https://hub.docker.com/repository/docker/glitchcrab/alpine-debug)
and [here](https://hub.docker.com/repository/docker/glitchcrab/alpine-debug).

Note: namespaces are not defined.

## Deploy

1. Deploy service account:
```bash
kubectl create -f https://raw.githubusercontent.com/glitchcrab/k8s-dbg-ymls/master/service-account.yaml
```
2. Deploy RBAC required to use the PodSecurityPolicy:
```bash
kubectl create -f https://raw.githubusercontent.com/glitchcrab/k8s-dbg-ymls/master/rbac.yaml
```
3. Deploy PodSecurityPolicy (if required):
```bash
kubectl create -f https://raw.githubusercontent.com/glitchcrab/k8s-dbg-ymls/master/pod-security-policy.yaml
```
4. Deploy NetworkPolicy (if required):
```bash
kubectl create -f https://raw.githubusercontent.com/glitchcrab/k8s-dbg-ymls/master/network-policy.yaml
```
5. Deploy pod
    1. As an unprivileged user:
    ```bash
    kubectl create -f https://raw.githubusercontent.com/glitchcrab/k8s-dbg-ymls/master/deployment-not-root.yaml
    ```
    2. As the root user:
    ```bash
    kubectl create -f https://raw.githubusercontent.com/glitchcrab/k8s-dbg-ymls/master/deployment-root.yaml
    ```

## Cleanup

```bash
kubectl delete -f https://raw.githubusercontent.com/glitchcrab/k8s-dbg-ymls/master/deployment-root.yaml
kubectl delete -f https://raw.githubusercontent.com/glitchcrab/k8s-dbg-ymls/master/deployment-not-root.yaml
kubectl delete -f https://raw.githubusercontent.com/glitchcrab/k8s-dbg-ymls/master/network-policy.yaml
kubectl delete -f https://raw.githubusercontent.com/glitchcrab/k8s-dbg-ymls/master/pod-security-policy.yaml
kubectl delete -f https://raw.githubusercontent.com/glitchcrab/k8s-dbg-ymls/master/rbac.yaml
kubectl delete -f https://raw.githubusercontent.com/glitchcrab/k8s-dbg-ymls/master/service-account.yaml
```
