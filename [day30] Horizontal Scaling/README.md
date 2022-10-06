# [day30] Horizontal Scaling/Vertical Scaling
### Horizontal Scaling/Vertical Scaling
在服務越來越多的時候，伺服器負載會越來越高，因此出現兩種擴展方式分別為，Horizontal scaling和vertical scaling。

Vertical Scaling(垂直擴展)
* 增加pod上的resource資源
* 增加node上的CPU/RAM資源

Horizontal Scaling(水平擴展)
* 增加pod數量
* 增加replica數量

#### Horizontal Pod Autoscaling
kubernetes提供Horizontal Pod Autoscaling，能根據自身容器的資源使用量來決定調用資源的容器，`backend.yaml`如下所示，當容器cpu資源使用量超過50%，會去新增pod
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: backend-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: backend
  template:
    metadata:
      labels:
        app: backend
    spec:
      containers:
      - name: my-pod
        image: backend:latest
        ports:
        - containerPort: 3000
        resources:
          requests:
            cpu: 200m
---
apiVersion: autoscaling/v1
kind: HorizontalPodAutoscaler
metadata:
  name: backend-hoz
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: backend-deployment
  minReplicas: 2
  maxReplicas: 5
  targetCPUUtilizationPercentage: 50
```

## 參考
* https://sean22492249.medium.com/kubernetes-horizontal-scaling-vertical-scaling-%E6%A6%82%E5%BF%B5-e8e70ce6f034
* https://ithelp.ithome.com.tw/articles/10197046

