# config-server
配置中心

> * 1、开启安全认证说明

>   >  具体可以查看 application.yml 配置文件中有对应的配置说明

> * 2、认证账号、密码，可以在环境变量中设定；
```
erueka.user
erueka.password
```


> * 3、关闭安全认证配置

>   > 需要在application.yml  配置文件中，修改defaultZone 的地址，具体修改如下：
```
 defaultZone: "http://localhost:${server.port}/eureka/"
```

> * 4、去除安全认证配置

>   > 需要在application.yml  配置文件中，修改一配置：
```
 1、修改注册中心地址：
 
     defaultZone: "http://localhost:${server.port}/eureka/"
     
 2、注释以下配置信息
 
   #spring:
   #  security:
   #    user:
   #      name: ${erueka.user:admin}
   #      password: ${erueka.password:admin001} 
   
 3、pom 文件中 spring-boot-starter-security 依赖去除

```
