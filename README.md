# Tikal Fuse-day: d'Artagnan Infrastructure

> Infrastructure as code repository for fuse-day, d'Artagnan team!

## Team

Name | Description
-----|-------------
Hila | 
Liya | 
Aya  | 
Ivan | 
Rafi | 

## Workstation Setup

```bash
brew install kubernetes-cli kubernetes-helm kubectx stern --with-short-names
brew upgrade kubernetes-cli kubernetes-helm kubectx stern
```

## Helm Init

```bash
helm repo update
kubectl apply -f rbac-config.yaml
helm init --service-account tiller
```

## Cert-manager

```bash
helm install --name cert-manager --namespace kube-system stable/cert-manager
```

## Registry

```bash
docker run --entrypoint htpasswd registry:2.6.2 -Bbn deploy "tikal" > htpasswd
kubectl create secret generic registry-auth-secret --from-file=htpasswd=htpasswd --namespace=kube-system
kubectl apply -f manifests/registry.yaml

kubectl create secret docker-registry regcred \
   --docker-server=docker.dartagnan.devops.fuse.tikal.io \
   --docker-username=deploy \
   --docker-password=tikal
```

## Metrics Server

```bash
helm upgrade metrics --install -f helm/metrics-server/values.yaml stable/metrics-server --namespace kube-system
```

## Nginx Ingress

```bash
helm upgrade ingress --install -f helm/nginx/values.yaml stable/nginx-ingress --namespace ingress
```

## Drone CI

```bash
kubectl create secret generic drone-server-secrets \
      --namespace=ci \
      --from-literal=DRONE_GITHUB_SECRET="******************************"

helm upgrade drone --install -f helm/drone/values.yaml stable/drone --namespace ci --set server.env.DRONE_GITHUB_CLIENT="********************"
```

## Ghost

```bash
helm upgrade blog --install -f helm/ghost/values.yaml stable/ghost --namespace default
```

## Prometheus

```bash
```
