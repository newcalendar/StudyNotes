# Springboot学习笔记

## 一、Springboot的简介

### 1、Springboot优点

1、相对于spring，springboot开发更为方便，springboot约定大于配置，可以用注解进行开发，不需要进行xml的配置

2、springboot基于spring开发，开箱即用，有内嵌的服务器 

### 2、springboot核心功能

1、起步依赖

2、自动配置

## 二、springboot的快速开发

1、创建Maven工程

2、导入起步依赖

3、创建springboot的启动类

```java
//启动类注解，声明为引导类
@SpringbootApplication
public class LearnApplication{
    
    //main方法是Java程序的入口
    public  void static main(args[] String){
        
        //run方法为运行引导类
        SpringApplication.run(LearnApplication.class);
    } 
}
```

4、编写具体业务逻辑

### 三、Springboot相关技术

#### 1、SPringboot热部署：

(1)添加一个热部署的依赖坐标，spring-boot-devtools

(2)在设置中->Compiler->Build project automatically

(3)Ctrl+Shift+Alt+/   ->Registry -> compiler automake.allow

#### 2、使用IDEA快速开发Springboot

在新建项目时选择Spring Initiallzr

#### 3、起步依赖

（1）不需要指定依赖版本号，对依赖做统一版本控制

#### 4、自动配置

1、将一些配置进行默认配置

###  四、Springboot的配置文件

1、application.yml或者是application.properties

(1)YML文件的后缀可以是yml或者yaml，比xml更为简洁

(2)用缩进代表层级关系

(3)优先级：yml->yaml->properties

2、Bootstrap.yml

Bootstrap.yml优先级高于application.yml

3、当在配置文件自定义配置，springboot不识别

(1)需要使用@Value进行获取

application.yml

```yaml
name: joke
```

test.java

```java
@Value("${name}")
private String name;

System.out.pritln(name);
```

结果：

```
joke
```



(2)使用@ConfigurationProperties来获取，可以获取整体数据

```java
@ConfigurationProperties(prefix="name")
```

### 五、Springboot整合Mybatis

添加Mybatis依赖和数据库驱动

```xml
<!--mybatis起步依赖-->
<dependency>
    <groupId>org.mybatis.spring.boot</groupId>
    <artifactId>mybatis-spring-boot-starter</artifactId>
    <version>1.1.1</version>
</dependency>
```

```xml
<!-- MySQL连接驱动 -->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
</dependency>
```

添加数据库配置

```yaml
spring
   datasource
     driverClassName：com.mysql.jdbc.Driver
     url：jdbc:mysql://127.0.0.1:3306/tb_name?
     username: root
     password: root
```

### 创建实体Bean

```java
public class User {
    // 主键
    private Long id;
    // 用户名
    private String username;
    // 密码
    private String password;
    // 姓名
    private String name;
  
    //此处省略getter和setter方法 .. ..
    
}
```

### 编写Mapper

```java
@Mapper
public interface UserMapper {
	public List<User> queryUserList();
}
```

注意：@Mapper标记该类是一个mybatis的mapper接口，可以被spring boot自动扫描到spring上下文中

###  配置Mapper映射文件

在src\main\resources\mapper路径下加入UserMapper.xml配置文件"

```xml
<?xml version="1.0" encoding="utf-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd" >
<mapper namespace="com.itheima.mapper.UserMapper">
    <select id="queryUserList" resultType="user">
        select * from user
    </select>
</mapper>
```

###  在application.properties中添加mybatis的信息

```properties
#spring集成Mybatis环境
#pojo别名扫描包
mybatis.type-aliases-package=com.itheima.domain
#加载Mybatis映射文件
mybatis.mapper-locations=classpath:mapper/*Mapper.xml
```

### 编写测试Controller

```java
@Controller
public class MapperController {

    @Autowired
    private UserMapper userMapper;

    @RequestMapping("/queryUser")
    @ResponseBody
    public List<User> queryUser(){
        List<User> users = userMapper.queryUserList();
        return users;
    }

}
```

### 整合Redis

添加redis依赖

```
<!-- 配置使用redis启动器 -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

配置redis信息

```
spring
  redis
     host：127.0.0.1
     port： 6379
```

注入RedisTemplate

  另：RedisTemplate常用方法

```
判断是否有key对应的值，返回Boolean值
redisTemplate.hasKey(Key)

有则取出对应值
redisTemplate.OpsForValue().get(Key)

设置过期时间
public Boolean expire(String key, long timeout, TimeUnit unit) {
    return redisTemplate.expire(key, timeout, unit);
 }


```

