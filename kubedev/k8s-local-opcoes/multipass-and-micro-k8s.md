## Multipass / Micro K8S

 Multipass / Micro K8S é uma ótima maneira de criar clusters Kubernetes para ambientes de desenvolvimento.


## Multipass 

Utilizado para criar e executa máquinas virtuais.

[https://multipass.run/](https://multipass.run/)

```
snap install multipass
```

```
multipass launch -n k8s -c 2 -m 2gb -d 20gb
multipass launch -n k8s2 -c 2 -m 4G -d 20G
```

```
-n => nome
-c => nucleos
-m => memória
-d => disco
```

```
multipass list
```

```
multipass shell k8s
```

```
multipass exec k8s -- touch test.txt
```

## MicroK8s

MicroK8s é o K8s de nível de produção mais simples, leve muito utilizado para ambiente de desenvolvimento 

Instalar K8s na máquina virtual criada com Multipass.
```
multipass exec k8s -- sudo snap install microk8s --classic --channel=1.18/stable
```

Habilita usuário ubuntu para usar K8s.
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
### _Importante_

Apontar kubectl local para k8s virtual criado com multipass
```
multipass exec k8s -- /snap/bin/microk8s.kubectl config view --raw
```
Copiar configuracoes para arquivo $HOME/.kube/config

---

### Adicionar um segundo node no cluster

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

Remove node
```
multipass shell k8s
microk8s remove-node k8s2

multipass shell k8s2
microk8s leave
```
