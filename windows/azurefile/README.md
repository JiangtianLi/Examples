# Create Azure File workload
This example is modified after https://github.com/andyzhangx/Demo/tree/master/windows/azurefile/rs3

## 1. Create an azure file storage class
```kubectl apply -f https://raw.githubusercontent.com/JiangtianLi/Examples/master/windows/azurefile/storageclass-azurefile.yaml```

#### make sure storageclass is created successfully
```
kubectl get storageclass/azurefile -o wide
```

## 2. Create a pvc for azure file
```kubectl apply -f https://raw.githubusercontent.com/JiangtianLi/Examples/master/windows/azurefile/pvc-azurefile.yaml```

#### make sure pvc is created successfully
```
kubectl get pvc/pvc-azurefile -o wide
```

## 3. Create a pod with azure file pvc
```kubectl apply -f https://raw.githubusercontent.com/JiangtianLi/Examples/master/windows/azurefile/iis-azurefile.yaml```

#### watch the status of pod until its `STATUS` is `Running`
```
watch kubectl get po/iis-azurefile -o wide
```

## 4. Enter the pod container to validate
```
kubectl exec -it iis-azurefile -- cmd
```

```
C:\>dir c:\mnt\azure
 Volume in drive C has no label.
 Volume Serial Number is F878-8D74

 Directory of c:\mnt\azure

11/16/2017  09:45 PM    <DIR>          .
11/16/2017  09:45 PM    <DIR>          ..
               0 File(s)              0 bytes
               2 Dir(s)   5,368,709,120 bytes free

```