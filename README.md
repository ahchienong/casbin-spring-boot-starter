# Casbin Spring Boot Starter

[![](https://raw.githubusercontent.com/casbin/jcasbin/master/casbin-logo.png)](https://casbin.org)

#### 传送门: [**jCasbin**](https://github.com/casbin/jcasbin)

Casbin Spring Boot Starter 用于帮助你在Spring Boot项目中轻松集成[jCasbin](https://github.com/casbin/jcasbin)。

## 如何使用
1. 在 Spring Boot 项目中加入```casbin-spring-boot-starter```依赖

```Maven```
```xml
<dependency>
   <groupId>com.github.fangzhengjin</groupId>
   <artifactId>casbin-spring-boot-starter</artifactId>
   <version>version</version>
</dependency>
```
```Gradle```
```groovy
implementation 'com.github.fangzhengjin:casbin-spring-boot-starter:version'
```
2. 添加配置
```yaml
casbin:
  #是否开启Casbin,默认开启
  enableCasbin: true
  #是否开启策略自动保存，如适配器支持该功能，默认开启
  autoSave: true
  #存储类型[file,jdbc]，目前支持的jdbc数据库[mysql(mariadb),h2,oracle,postgresql]
  #欢迎编写并提交您所使用的jdbc适配器，参见：org.casbin.adapter.OracleAdapter
  #jdbc适配器将主动寻找您在spring.datasource配置的数据源信息
  #默认使用jdbc,并使用内置h2数据库进行内存存储
  storeType: jdbc
  #数据源初始化策略[create(自动创建数据表,如已创建则不再进行初始化),never(始终不进行初始化)]
  initializeSchema: create
  #本地模型配置文件地址,约定默认读取位置:classpath:casbin/model.conf
  model: classpath:casbin/model.conf
  #如默认位置未找到模型配置文件,且casbin.model未正确设置,则使用内置默认rbac模型,默认生效
  useDefaultModelIfModelNotSetting: true
  #本地策略配置文件地址,约定默认读取位置:classpath:casbin/policy.csv
  #如默认位置未找到配置文件，将会抛出异常
  #该配置项仅在storeType设定为file时生效
  policy: classpath:casbin/policy.csv
  #是否开启CasbinWatcher机制,默认不开启
  enableWatcher: false
  #CasbinWatcher通知方式,默认使用Redis进行通知同步,暂时仅支持Redis
  #开启Watcher后需手动添加spring-boot-starter-data-redis依赖
  watcherType: redis
```
3. 最简配置
```yaml
casbin:
  #如果您使用的模型配置文件位于此地址,则无需任何配置
  model: classpath:casbin/model.conf
```
##### 注意: 如果您没有设置其他数据源,或为H2设定存储文件位置,则默认使用H2将数据存储于内存中