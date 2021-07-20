## K3D

k3d é um wrapper leve para executar k3s (distribuição mínima do Kubernetes do Rancher Lab) no docker.

O k3d torna muito fácil criar clusters k3s de um e vários nós no docker, por exemplo, para desenvolvimento local no Kubernetes.

```
k3d cluster create --config ./k3d/cluster-kubernetes.yaml
```