## Kind

kind é uma ferramenta para executar clusters Kubernetes locais usando "nós" de contêiner do Docker.

Install
```
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.11.1/kind-linux-amd64
chmod +x ./kind
mv ./kind /some-dir-in-your-PATH/kind
```

Create
```
kind create cluster
or
kind create cluster --name name-cluster
```

Test
```
kind get clusters
kubectl get nodes
docker container ls
```

Delete 
```
kind delete cluster
or
kind delete name-cluster
```

## Criar cluster com base em especificação .yaml
```yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
- role: worker
- role: worker
```

```
kind create cluster --config name.yaml --name cluster-kubernetes
```
