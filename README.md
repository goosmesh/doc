# doc
goos 开发部署

#### goos简介
  goos项目大体分为两部分，
  goos 服务端（goos）
  goos 边车（goossidecar）
  
### 推荐部署模式
  goos的核心是dns服务器，goos和goossidecar都是基于coredns开发的，想要goos可以通讯，至少要配置：
  1、goossidecar到goos服务器的ip连接
  2、goos边车dns抽象sidecar.goos. -> 127.0.0.1
  3、goos服务器dns抽象server.goos. -> goos server ip list
  
  
#### 开始使用
  待完善
