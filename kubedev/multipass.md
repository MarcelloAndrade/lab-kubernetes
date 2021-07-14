## Multipass

Cria e executa máquinas virtuais 

```
snap install multipass
```

```
multipass launch -n k8s -c 2 -m 2gb -d 20gb
```

```
-n => nome
-c => nucleos
-m => memoria
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