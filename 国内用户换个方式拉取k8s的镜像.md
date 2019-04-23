1、登录google的CloudShell `https://console.cloud.google.com/cloudshell`

2、拉取k8s的镜像比如`apiserver`
```
docker pull k8s.gcr.io/kube-apiserver:v1.14.1
```
3、登录阿里云控制台->`https://cr.console.aliyun.com/cn-shenzhen/instances/repositories`->
镜像仓库->创建镜像仓库->仓库名称保持跟k8s一致`kube-apiserver`->点击`管理`

4、在Google的CloudShell中输入
```
# 在CloudShell中登录阿里云仓库镜像服务
sudo docker login --username=amour871 registry.cn-shenzhen.aliyuncs.com -> 然后输入登录密码（非阿里云登录密码）

# 将k8s的tag修改为如下
sudo docker tag [ImageId] registry.cn-shenzhen.aliyuncs.com/xuxuzhaozhao/kube-apiserver:[镜像版本号]
sudo docker tag k8s.gcr.io/kube-apiserver:v1.14.1 registry.cn-shenzhen.aliyuncs.com/xuxuzhaozhao/kube-apiserver:v1.14.1

# 推送到阿里云中
 sudo docker push registry.cn-shenzhen.aliyuncs.com/xuxuzhaozhao/kube-apiserver:[镜像版本号]
 sudo docker push registry.cn-shenzhen.aliyuncs.com/xuxuzhaozhao/kube-apiserver:v1.14.1
```

5、在自己的centos中（虚拟机、vps、自己的服务器）
```
# 拉取自己阿里云的镜像
docker pull registry.cn-shenzhen.aliyuncs.com/xuxuzhaozhao/kube-apiserver:v1.14.1

# 修改为k8s的tag
docker tag registry.cn-shenzhen.aliyuncs.com/xuxuzhaozhao/kube-apiserver:v1.14.1 k8s.gcr.io/kube-apiserver:v1.14.1

# 移除阿里云的tag
docker rmi -f registry.cn-shenzhen.aliyuncs.com/xuxuzhaozhao/kube-apiserver:v1.14.1
```

6、这下服务器就有k8s的镜像了