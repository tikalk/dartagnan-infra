# Tikal Fuse-day: Dartagnan-infra

> Infra repo for fuse Dartagnan group

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

## Metrics Server

```bash
helm install -f helm/metrics-server/values.yaml stable/metrics-server --name metrics --namespace kube-system
```

## Nginx Ingress

```bash
helm install -f helm/nginx/values.yaml stable/nginx-ingress --name ingress --namespace ingress
```

## Drone CI

```bash
helm install -f helm/drone/values.yaml stable/drone --name drone --namespace ci
kubectl create secret generic drone-server-secrets \
      --namespace=ci \
      --from-literal=DRONE_GITHUB_SECRET="******************************"

  helm upgrade drone \
      --reuse-values \
      --set server.env.DRONE_PROVIDER="github" \
      --set server.env.DRONE_GITHUB="true" \
      --set server.env.DRONE_ORGS="tikalk" \
      --set server.env.DRONE_GITHUB_CLIENT="***************" \
      --set server.envSecrets.drone-server-secrets[0]=DRONE_GITHUB_SECRET \
      stable/drone
```

## Ghost

```bash
```

## Prometheus

```bash
```
