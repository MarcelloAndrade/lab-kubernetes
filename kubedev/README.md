## Docker

## Kubectl

```
kubectl version --short
```

## Multipass
[install](multipass.md)

## MicroK8s
Cria maquina para rodar o K8s - (NODE no cluster)
```
multipass launch -n k8s -c 2 -m 4G -d 20G
```

Instala K8s na maquina virtual criada
```
multipass exec k8s -- sudo snap install microk8s --classic --channel=1.18/stable
```

Habilita usuario ubuntu para usar K8s
```
multipass exec k8s -- sudo usermod -a -G microk8s ubuntu
multipass exec k8s -- sudo chown -f -R ubuntu ~/.kube
multipass restart k8s
```

Teste create pod nginx
```
multipass exec k8s -- /snap/bin/microk8s.kubectl create deployment nginx --image nginx

multipass exec k8s -- /snap/bin/microk8s.kubectl get pods
```

----
### - _Importante_

Apontar kubectl local para k8s virtual criado com multipass
```
multipass exec k8s -- /snap/bin/microk8s.kubectl config view --raw
```
Copiar configuracoes para arquivo $HOME/.kube/config

---

### - _Adicionar um segundo node no cluster_

 - Repita os passos para criar um microk8s e suas configuracoes
 - Entre no node principal via multipass e execute o comando _microk8s add-node_
```
multipass shell k8s
microk8s add-node
```
 - Copie o _join_ no segundo node criado  
```
multipass shell k8s2
microk8s join 10.26.195.19:25000/NBDrXawDhswGbdHeSQBzqdGwcfpAaOPcBux
```

---

Test kubectl local
```
kubectl get nodes
```


