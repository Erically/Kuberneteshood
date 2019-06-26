#### harbor安装过程

```
a.clone代码
# git clone https://github.com/goharbor/harbor-helm.git
# cd harbor-helm
就安装master分支

b.修改values.yaml文件
# vi values.yaml
参数修改：
host: core.harbor.172.16.20.76.nip.io
externalURL: https://core.harbor.172.16.20.76.nip.io
storageClass: fast-disks

c.helm安装
# helm install --namespace=harbor --name=harbor ./

d.测试
访问地址https://core.harbor.172.16.20.76.nip.io

e.其他
vi中全文替换用法：%s/node1/node4/g
如果重新安装，记得删除原来的pvc，再安装

```