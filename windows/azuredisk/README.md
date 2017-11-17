# Create Azure Disk workload
This example is modified after https://github.com/andyzhangx/Demo/tree/master/windows/azuredisk/rs3

## 1. Create an azure disk storage class

### option#1: k8s agent pool is based on blob disk VM
```kubectl apply -f https://raw.githubusercontent.com/JiangtianLi/Examples/master/windows/azuredisk/storageclass-azuredisk.yaml```

### option#2: k8s agent pool is based on managed disk VM
```kubectl apply -f https://raw.githubusercontent.com/JiangtianLi/Examples/master/windows/azuredisk/storageclass-azuredisk-managed.yaml```

#### make sure storageclass is created successfully
```
kubectl get storageclass/azuredisk -o wide
```

## 2. Create a pvc for azure disk
```kubectl apply -f https://raw.githubusercontent.com/JiangtianLi/Examples/master/windows/azuredisk/pvc-azuredisk.yaml```

#### make sure pvc is created successfully
```
kubectl get pvc/pvc-azuredisk -o wide
```

## 3. Create a pod with azure disk pvc
```kubectl apply -f https://raw.githubusercontent.com/JiangtianLi/Examples/master/windows/azuredisk/iis-azuredisk.yaml```

#### watch the status of pod until its `STATUS` is `Running`
```
watch kubectl get po/iis-azuredisk -o wide
```

## 4. Enter the pod container to validate
```
kubectl exec -it iis-azuredisk -- cmd
```
