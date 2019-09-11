#### turn on Preset

- 什么是Preset
```
Preset的作用：
Preset保存的是一些配置，这些配置会根据label seclector自动加载进匹配的pod中，不用在pod中添加关于Preset的任何内容
```

- 停止kube-apiserver

```
# systemctl stop kube-apiserver
```

- 配置kube-apiserver

```
# vim /etc/systemd/system/kube-apiserver.service

在runtime后面添加settings.k8s.io/v1alpha1=true，如下
--runtime-config=batch/v2alpha1=true,settings.k8s.io/v1alpha1=true

在admission-control后面添加PodPreset,如下
--admission-control=NamespaceLifecycle,LimitRanger,ServiceAccount,DefaultStorageClass,ResourceQuota,NodeRestriction,PodPreset
```

- 重新启动kube-apiserver

```
# systemctl restart kube-apiserver
```

- 查看启动状态和日志

```
# systemctl status kube-apiserver
# journalctl -u kube-apiserver -f
```

- 验证PodPreset打开
  
```
# kubectl api-resources|grep podpreset
```

- PodPreset的使用见同文件夹下的yml文件

```
1.可用来预先配置环境变量
2.可用来预先配置volumes
3.可用来预先配置voulmeMounts
...

例子以设置时区为例，主要有两种方式配置container时区，一种环境变量，一种宿主机/etc/localtime挂载，
两种方式都可以在pod中直接操作，或借助preset进行预配置
```
