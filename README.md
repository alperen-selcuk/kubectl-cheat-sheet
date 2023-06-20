# kubectl-cheat-sheet

## run
pod yaratmak için kullanılır

```kubectl run nginx --image=nginx```

## create
kubernetes resource yaratmak için kullanılır.

```kubectl create deployment nginx --image=nginx```

## expose
deployment ve pod a erişim için service objesi oluşturmak için kullanılır.

```kubectl expose pod nginx --port=80```

## edit
anlık olarak kubernetes resourcelarını değiştirmek için kullanılır.

```kubectl edit deployment web``` 

## set image
kubernetes deployment veya pod üzerinde image i değiştirmek için kullanılır. 

```kubectl set image deployment/web web=nginx```

## rollout 
kuberentes deploymentinizin önceki versiyonlarını görüntülemek, o versiyonlara geri dönmek ve  mevcut versiyonda podları yeniden başlatmak için kullanılır.

```
kubectl rollout history deployment/web

kubectl rollout undo deployment/web --to-revision=2

kubectl rollout restart deployment/web
```

## scale
mevcut deployment da replica sayısını değiştirmek için kullanılır

```kubectl scale --replicas=3 deployment/web```

## cp
kubernetes podu içine lokalden dosya atmak için veya pod içinden lokale dosya atmak için kullanılır.

```
kubectl cp default/web:/var/deneme.txt ~/deneme.txt

kubectl cp abc.txt default/web:/var/abc.txt
```

## port-forward
en kolay şekilde lokalden kubernetes servisine erişmek için kullanılır.

```kubectl port-forward svc/web 8080:80```

## label
kubernetes resourlarına label vermek için kullanılır.

```kubectl label pods web platform=www```

## cordon ve uncordon
kubernetes nodelarını pod schedule edilmemesini ve edilmesini belirtirsiniz.

```kubectl cordon node``` 
```kubectl uncordon node```
