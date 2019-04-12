# 概念
    这里给出几个概念
    1、node：代表一个linux实体（当然也可以是linux docker容器），node是一种特殊的container，他上面也会有sidecar，但是和具体业务的边车稍微不一样（插件不一样），主要表现在dns的处理、支持使用goos api部署服务（动态修改、创建、删除容器）；
    2、container：这里的container是一个虚化的概念，一个container由一个sidecar和一个docker（目前只设想docker）容器，也就是说一个container是一个mesh节点；
    3、goos manager：goos的核心管理，集成了所有的核心插件，ui，由于ha相对独立，这里不考虑ha；
    

# 总体部署架构
    总统架构是goos manager <---> node goos sidecar <---> container goos sidecar <---> docker(service)
    
    1、关于配置文件，配置文件，goos希望是完全由manager管理，由于container的部署是由manager管理的，因此manager会在部署的时候注入配置文件；
    2、服务注册，服务注册主要由container sidecar负责，由于container的部署是由manager创建，所以可以通过元信息由container sidecar完成注册，注册时初步设想是修改ipvs实现域名-ip、端口-服务的映射；
    3、服务发现，由于使用dns和ipvs，这里http、https可以实现透明访问，至于grpc、dubbo、sofa这些，由于未深入思考，暂不考虑；
