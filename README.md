# kubectl-cheat-sheet

## run
pod yaratmak için kullanılır

```
kubectl run nginx --image=nginx
```

## create
kubernetes resource yaratmak için kullanılır.

```
kubectl create deployment nginx --image=nginx
```

## dry-run

bir resourceu yaratırmış gibi yapmak anlamına gelir. kubernetes api ye isteği göndermez, ne göndereceğini detaylı görmek için de -oyaml ile kullanılır. hatta istenirse bir dosyaya atılabilir özellikle sınavlarda çok işe yarar.

```
kubectl create deployment nginx --image=nginx --dry-run=client  -oyaml
kubectl create deployment nginx --image=nginx --dry-run=client  -oyaml > deployment.yaml
```

## describe

bir kubernetes resource u hakkında detaylı bilgi almak için kullanılır. genellikle troubleshoot zamanı çok işimize yarar.

```
kubectl describe pod nginx
```

## expose
deployment ve pod a erişim için service objesi oluşturmak için kullanılır. 

```
kubectl expose pod nginx --port=80
```

eğer container port farklı ise target port olarak belirtmeniz gerek
```
kubectl expose deployment/nginx --port=80 --target-port=8080
```

herhangi bir şey belirtmezseni ClusterIP açar. type ı belirtmeniz gerek.

```
kubectl expose deployment/nginx --port=80 --type=LoadBalancer
```

## edit
anlık olarak kubernetes resourcelarını değiştirmek için kullanılır.

```
kubectl edit deployment web
``` 

## set image
kubernetes deployment veya pod üzerinde image i değiştirmek için kullanılır. kubernetes deployment ile container isminiz aynı olması lazım. 

```
kubectl set image deployment/web web=nginx
```

## rollout 
kuberentes deploymentinizin önceki versiyonlarını görüntülemek, o versiyonlara geri dönmek ve  mevcut versiyonda podları yeniden başlatmak için kullanılır.

```
kubectl rollout history deployment/web

kubectl rollout undo deployment/web --to-revision=2

kubectl rollout restart deployment/web
```

## scale
mevcut deployment da replica sayısını değiştirmek için kullanılır

```
kubectl scale --replicas=3 deployment/web
```

## cp
kubernetes podu içine lokalden dosya atmak için veya pod içinden lokale dosya atmak için kullanılır.

```
kubectl cp default/web:/var/deneme.txt ~/deneme.txt

kubectl cp abc.txt default/web:/var/abc.txt
```

## port-forward
en kolay şekilde lokalden kubernetes servisine erişmek için kullanılır. sizin local portunuza kubernetes poduna veya servisine doğru tunnel açar

```
kubectl port-forward svc/web 8080:80
kubectl port-forward pod nginx 8888:80
```


## label
kubernetes resourlarına label vermek için kullanılır. sonradan bu labelları pod/node affinity, taint/toleration gibi yerlerde kullanabilirsiniz.

```
kubectl label pods web platform=www
kubectl label nodes node-1 system=ubuntu
```

## set-context namespace

sürekli çalıştığınız namespace varsa ve sürekli -n --namespace selectorleri girmek istemiyorsanız sabitlemek için kullanılır. özellikle kubernetes sınavlarında

```
kubectl config set-context --current --namespace production
```

## cordon ve uncordon
kubernetes nodelarını pod schedule edilmemesini ve edilmesini belirtirsiniz. cordon schedule e kapatır uncordon geri açar.

```kubectl cordon node```  

```kubectl uncordon node```

## drain

kubernetes node üzerindeki podları diğer nodelara aktarılmasını sağlar. genellikle node upgradelerinde kullanılır. 
daemonset varsa kubernetes de çalışan  ignore komutu ile kullanılması gerekir.
```
kubectl drain node-1 --ignore-daemonsets
```

