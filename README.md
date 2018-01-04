### 自动构建docker


	kubernetes-dashboard-amd64



在 github 创建一个 repository，里面有一个 Dockerfile

	FROM gcr.io/google_containers/kubernetes-dashboard-amd64:v1.8.4
	MAINTAINER zouhuigang <zouhuigang888@gmail.com>


登录docker hub:

	https://hub.docker.com/

选择create-> Create Automated Build->Link Accounts->Link Github->Select->github登录授权

再次选择Create Automated Build点击github会获取github所有的项目。


搜索我们的项目:kubernetes-dashboard-amd64,点击进去


![image](./images/20180103195308.png)


点击create!


完成之后，得到镜像:


	https://hub.docker.com/r/952750120/kubernetes-dashboard-amd64/


![image](./images/20180104113229.png)





### 问题：

Q1：docker hub构建失败

	Building in Docker Cloud's infrastructure...
	Cloning into '.'...

	Dockerfile not found at ./Dockerfile


A1：

	将DOCKERFILE重命名为:Dockerfile
	需要先将github库中的DOCKERFILE删除掉，再增加，不然不会重命名:Dockerfile,提交成功之后dockerhub会自动构建镜像。


Q2：

	Build failed: manifest for gcr.io/google_containers/kubernetes-dashboard-amd64:v1.8.4 not found


A2：

	改成gcr.io/google_containers/kubernetes-dashboard-amd64:v1.8.1



Q3:

自动构建的镜像，怎么自动打上tag标签。

A3:

![image](./images/20180104112815.png)

之后提交git用:

	git add -A
	git commit -am "测试自动构建标签"
	git tag -a v1.8.1 -m 'kubernetes-dashboard-amd64:v1.8.1' #此标签只是创建tag的，已有tag不需要执行这条命令
	git push origin v1.8.1


