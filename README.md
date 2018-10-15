# istio-ui

## &nbsp;&nbsp;&nbsp;&nbsp;istio-ui用于管理istio配置文件，目的是减轻运维的配置工作。主要实现：注入，istio配置和模板（还在开发中）等功能。
## 为了保证注入和配置的原生性，参考是使用了istio的源码。


### 三种注入方式
* 一键注入
  > 基于运行中的服务```Deployment:apps/v1```进行注入，使用这种方式服务会被重新部署
* 文件上传注入
  > 将你需要注入的文件发送到远程api接口
  
  > kubectl apply -f <(curl -F "config=@samples/bookinfo/platform/kube/bookinfo.yaml" http://localhost:9100/inject/file)
* 文件内容注入
  > 将你需要注入的内容发送到远程api接口
  
  > kubectl apply -f <(curl -X POST --data-binary @samples/bookinfo/platform/kube/bookinfo.yaml -H "Content-type: text/yaml" http://localhost:9100/inject/context)


### 安装
> 安装前先确认已安装k8s
* docker
> &nbsp;&nbsp;&nbsp;&nbsp;设置 [KUBECONFIG](https://kubernetes.io/docs/tasks/access-application-cluster/configure-access-multiple-clusters/#create-a-second-configuration-file)

> &nbsp;&nbsp;&nbsp;&nbsp;docker run -itd -v $KUBECONFIG:$HOME/.kube/config -p9100:9100 --name istio-ui --env KUBECONFIG=$HOME/.kube/config istio-ui

* k8s
> &nbsp;&nbsp;&nbsp;&nbsp;kubectl apply -f ./istio-ui.yaml
