```
❓An existing Pod needs to be integrated into the kubernetes built-in logging architecture(e.g. kubectl logs).
Adding a streaming sidecar container is a good and common way to accomplish this requirement.
Task:
- Add a sidecar container named sidecar, using the busybox image, to the existing Pod eshop-cart-app. 
- The new sidecar container has to run the following command: /bin/sh -c "tail -n+1 -F /var/log/cart-app.log"
- Use a Volume mounted at /var/log, to make the log file cart-app.log available to the sidecar container. 
- Don't modify the cart-app
```

![image](https://github.com/PragmaticArchive/CKA/assets/58178752/eb7e9273-667d-40df-b95f-37ee415fd8b9)
```yaml
사이드카 컨테이너: 하나의 pod안에서 두개의 컨테이너와 volume이 같이 만들어져서 동작
동작중인 eshop-cart-app의 log(access.log, error.log)를 다시 가공,분석해서 사용할 필요가 있을때 사이드카 컨테이너를 운영할 수 있음
```


```yaml
kubectl get pods eshop-cart-app
kubectl get pods eshop-cart-app -o yaml > eshop-cart-app.yaml

apiVersion: v1
kind: Pod
metadata:
  name: eshop-cart-app
spec:
  containers:
  - command:
    - /bin/sh
    - -c
    - 'i=1;while :;do echo -e "$i: Price: $((RANDOM % 10000 + 1))" >> /var/log/cart-app.log;
      i=$((i+1)); sleep 2; done'
  - name: cart-app
    image: busybox
    volumeMounts:
    - name: varlog
      mountPath: /var/log
  - name: sidecar
    image: busybox
    args: [/bin/sh, -c, 'tail -n+1 -F /var/log/cart-app.log']
  volumes:
  - name: varlog
    emptyDir: {}

kubectl apply -f eshop-cart-app.yaml
```
