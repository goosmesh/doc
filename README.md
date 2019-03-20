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
##### 编译goos
    1、下载goos源码git clone https://github.com/goosmesh/goos.git；
    2、编译打包cd {project_root}/build && ./build.sh
    3、初始化mysql数据库，下载数据库sql，本地创建数据库；
    4、初始化redis，在数据库中添加goos.的hash，增加两个键值对sidecar和server,
    值都为{"a":[{"ttl":300,"ip":"127.0.0.1"}]}；
    5、在Corefile中配置goos（mysq，端口等）数据库为goos.database（默认值root:1234@tcp(127.0.0.1:3306)/goos），
    端口为goos.port（默认值为4321）
    6、在Corefile中配置redis
    7、启动goos ./coredns
    
#### 编译goossidecar
    1、下载goossidecar源码git clone https://github.com/goosmesh/goossidecar.git；
    2、编译打包cd {project_root}/build && ./build.sh
    3、配置forward到goos中的coredns地址
    4、启动goossidecar ./coredns

#### 测试
    1、将本机的dns服务器设置为127.0.0.1
    2、下载spring clould alibaba 项目
    git clone https://github.com/spring-cloud-incubator/spring-cloud-alibaba.git找到例子中的nacos配置项目，
    将其nacos服务器位置设置为server.goos:4321
    3、在goos中添加config：网页打开http://server.goos:4321/desk/index.html；用户名：goos；密码：goos；
    在配置项中添加配置dataID为nacos-config-example.properties,groupID为DEFAULT_GROUP；并添加两个配置项 
    user.name=goos user.age=1
    4、启动nacos配置文件的例子，一切正常的话，可以看到数据库输出了我们在goos上配置的属性；

  待完善
