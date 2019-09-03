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

# actuator 指标监控说明

本栗子使用的springboot 2.1.7.RELEASE 版本，相对于2.0 以下版本配置信息查看有比较大的区别
```
  1、查看所有监控值汇总信息
  
     http://ip:port/actuator/prometheus
     
  2、在Spring Boot 2.0 中对Actuator变动很大，默认只提供/self，/health，/info这三个接口，如果想提供所有接口需要配置配置之后重新访问/actuator就会暴露出所有接口.
     
  【必须在yml配置文件新增以下配置】：
  management:
       endpoints:
           web:
               exposure:
                   include: "*"
            
   [验证：再对配置文件进行更改之前，可以访问：http://ip:port/actuator 查看效果]
            
  3、SpringBoot1.x的metrics信息
  
     http://ip:port/metrics
     
  {
      "mem":568029,
      "mem.free":164376,
      "processors":16,
      "instance.uptime":223643888,
      "uptime":223835542,
      "systemload.average":0.18,
      "heap.committed":415232,
      "heap.init":419840,
      "heap.used":250855,
      "heap":415232,
      "nonheap.committed":156480,
      "nonheap.init":2496,
      "nonheap.used":152797,
      "nonheap":0,
      "threads.peak":114,
      "threads.daemon":99,
      "threads.totalStarted":234,
      "threads":113,
      "classes":15474,
      "classes.loaded":15474,
      "classes.unloaded":0,
      "gc.ps_scavenge.count":1808,
      "gc.ps_scavenge.time":99224,
      "gc.ps_marksweep.count":3,
      "gc.ps_marksweep.time":5314
  }
  
  4、SpringBoot2.x的metrics信息 ,地址栏多加了一级目录：actuator
  
       http://ip:port/actuator/metrics
       
  {
      "names":[
          "jvm.memory.committed",
          "http.server.requests",
          "jvm.buffer.memory.used",
          "jvm.gc.memory.allocated",
          "tomcat.sessions.created",
          "tomcat.sessions.expired",
          "jvm.memory.used",
          "tomcat.global.error",
          "jvm.gc.max.data.size",
          "system.cpu.count",
          "jvm.memory.max",
          "tomcat.global.sent",
          "jvm.buffer.total.capacity",
          "jvm.buffer.count",
          "process.files.max",
          "jvm.threads.daemon",
          "process.start.time",
          "tomcat.sessions.active.max",
          "tomcat.global.request.max",
          "jvm.gc.live.data.size",
          "process.files.open",
          "process.cpu.usage",
          "tomcat.threads.current",
          "tomcat.servlet.request",
          "jvm.gc.pause",
          "process.uptime",
          "tomcat.threads.busy",
          "system.load.average.1m",
          "tomcat.cache.hit",
          "tomcat.global.request",
          "tomcat.servlet.error",
          "tomcat.servlet.request.max",
          "tomcat.cache.access",
          "tomcat.sessions.active.current",
          "system.cpu.usage",
          "jvm.threads.live",
          "jvm.classes.loaded",
          "jvm.classes.unloaded",
          "jvm.threads.peak",
          "tomcat.threads.config.max",
          "jvm.gc.memory.promoted",
          "tomcat.sessions.rejected",
          "tomcat.global.received",
          "tomcat.sessions.alive.max"
      ]
  }
  
  细节查看： http://ip:port/actuator/metrics/jvm.threads.peak
```
