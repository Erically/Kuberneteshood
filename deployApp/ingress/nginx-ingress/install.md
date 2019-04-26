#### nginx-ingress安装过程

- 获取values.yaml文件

`# curl -O https://raw.githubusercontent.com/helm/charts/master/stable/nginx-ingress/values.yaml`

- 修改配置文件

`# vi values.yaml`

```
hostnetwork: true
daemonset:
  useHostPort: true
```

- 安装nginx-ingress

`# helm install --name nginx-ingress stable/nginx-ingress --namespace=nginx-ingress -f values.yml`

- 安装测试应用

`# kubectl apply -f nginx.yml`
```
nginx.yml
---
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      run: nginx
  template:
    metadata:
      labels:
        run: nginx
    spec:
      containers:
      - image: nginx
        imagePullPolicy: Always
        name: nginx
        ports:
        - containerPort: 80
          protocol: TCP
      restartPolicy: Always
---
apiVersion: v1
kind: Service
metadata:
  name: nginx
spec:
  ports:
  - port: 80
    protocol: TCP
    targetPort: 80
  selector:
    run: nginx
  sessionAffinity: None
---
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: nginx
  annotations:
    kubernetes.io/ingress.class: nginx
spec:
  rules:
  - host: foo.test.com
    http:
      paths:
      - path: /
        backend:
          serviceName: nginx
          servicePort: 80

```

- 浏览器访问域名测试

```
http://foo.test.com
需要本地机子能够获取这个域名的ip地址，如果不能，需要自己在/etc/hosts配置[Linux]或C:\Windows\System32\drivers\etc配置[Windows]
```