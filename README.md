Docker Images Pusher

使用Github Action将国外的Docker镜像转存到阿里云私有仓库，供国内服务器使用，免费易用
支持DockerHub, gcr.io, k8s.io, ghcr.io等任意仓库
支持最大40GB的大型镜像
使用阿里云的官方线路，速度快
使用方式

配置阿里云

登录阿里云容器镜像服务
https://cr.console.aliyun.com/
启用个人实例，创建一个命名空间（NAME_SPACE） 
访问凭证–>获取环境变量
用户名（REGISTRY_USER)
密码（REGISTRY_PASSWORD)
仓库地址（REGISTRY）


Fork本项目

Fork本项目
启动Action

进入您自己的项目，点击Action，启用Github Action功能
配置环境变量

进入Settings->Secret and variables->Actions->New Repository secret  将上一步的四个值
NAME_SPACE,REGISTRY_USER，REGISTRY_PASSWORD，REGISTRY
配置成环境变量

添加镜像

打开images.txt文件，添加你想要的镜像 可以加tag，也可以不用(默认latest)
可添加 --platform=xxxxx 的参数指定镜像架构
可使用 k8s.gcr.io/kube-state-metrics/kube-state-metrics 格式指定私库
可使用 #开头作为注释

 文件提交后，自动进入Github Action构建
使用镜像

回到阿里云，镜像仓库，点击任意镜像，可查看镜像状态。(可以改成公开，拉取镜像免登录) 
在国内服务器pull镜像, 例如：
docker pull registry.cn-hangzhou.aliyuncs.com/shrimp-images/alpine
registry.cn-hangzhou.aliyuncs.com 即 REGISTRY(阿里云仓库地址)
shrimp-images 即 NAME_SPACE(阿里云命名空间)
alpine 即 阿里云中显示的镜像名
多架构

需要在images.txt中用 --platform=xxxxx手动指定镜像架构 指定后的架构会以前缀的形式放在镜像名字前面 


定时执行

修改/.github/workflows/docker.yaml文件 添加 schedule即可定时执行(此处cron使用UTC时区) 
