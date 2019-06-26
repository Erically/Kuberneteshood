#### curator 资料
```
1.ES官方推荐的索引生命周期管理软件
2.可以删除过期n天的索引
3.需要定时执行这个curator命令，所以使用k8s的pod管理器或job管理器cronjob(实际上cronjob直接管理的是job，job管理的pod)
4.相关链接：
阿里 https://www.alibabacloud.com/help/zh/doc-detail/107289.htm
cn-blogs https://www.cnblogs.com/crazymagic/p/10571259.html
```