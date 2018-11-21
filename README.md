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
helm init
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
```

## Ghost

```bash
```

## Prometheus

```bash
```
