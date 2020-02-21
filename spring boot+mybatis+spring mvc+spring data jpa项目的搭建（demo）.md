---
title: spring boot+mybatis+spring mvc+spring data jpa项目的搭建（demo）
date: 2019-12-17 13:33:12
tags:
- java
- spring
- spring boot
- spring data jpa
- spring mvc
- mybatis
categories: 
- 教程
- demo
---

# 前言

随着时代的飞速发展，ssh（struts2+spring+hibernate）曾是java企业开发的三大框架，但是其中struts2框架的漏洞问题和hibernate的查询效率问题等一系列原因导致三大框架进化成了ssm（spring mvc+spring+mybatis），但不管怎么变，庞大的配置文件是每一个java程序员的痛，在启动项目之前，你就需要花费大量精力来进行项目的配置，关键是这些配置大多数还是多数项目共通的，那么“配置”这个行为就变成了“复制粘贴”，这是毫无意义的，浪费时间的事情。这时，spring boot出世了，它解决了配置文件过多和依赖关系不好管理的问题，既“自动配置”和“热插拔”。本文内容为一个spring boot+mybatis+spring mvc+spring data jpa项目的小demo。

# 开始

打开idea
选择spring boot启动
在start那选择你要添加的组件（mybatis+spring mvc+spring data jpa+jdbc）
在application类同目录下创建service，dao，controller文件夹

# Controller 内容
```java
@RestController
@RequestMapping("/smp")
public class UserControlelr {

    @Autowired
    UserService userService;
    @ApiImplicitParams({
            @ApiImplicitParam(name="size",value="本页条数",dataType="Integer", paramType = "query",example="1")
    })
    @GetMapping("/selectUsers") /@PostMapping/@DeleteMapping/@PutMapping
    public Page<User> selete(Integer page,@ApiParam(name="大小",value="传入int格式",required=true)Integer size){
        return users;
    }
}
```

# Service内容
## Impl文件夹
```java
@Transactional
@Service
public class UserServiceImp implements UserService
{
    @Autowired
    User_repository user_repository;
    @Override
    public Page<User> selectUser(Integer page,Integer size) {
        page-=1;
        Sort orders = new Sort(Sort.Direction.ASC,"number");//已经进行更新，构造方法已经被私有化，不可以直接创建，直接调用静态方法就行
        Pageable of = PageRequest.of(page, size,orders);
        Page<User> all = user_repository.findAll(of);
        return all;
    }

    @Override
    public User insertUser(User user) {
        User save = user_repository.save(user);
        return save;
    }

    @Override
    public User updataUser(User user,Integer id) {
        user.setId(id);
        User save = user_repository.save(user);
        return save;
    }

    @Override
    public User deleteUser(Integer id) {
        Optional<User> byId = user_repository.findById(id);
        User user = byId.get();
        user_repository.deleteById(id);
        return user;
    }
}
```

# Dao内容
```java
public interface User_repository extends JpaRepository<javabean,主键>, JpaSpecificationExecutor<javabean> {
@Query(value ="select xxx from xxx where id=?1")
public xxx demo(int id);

}
```

# Entity内容
```java
@Entity
@ApiModel(value="user对象",description="用户对象user")
@Table(name = "usersmp")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    @ApiModelProperty(hidden = true)
    private Integer id;

    @Column(name = "name")
    @ApiModelProperty(value="用户名",name="name",example="xingguo")
    private String name;
 }
```

# Swagger2内容
```java
Configuration
@EnableSwagger2
public class Swagger2 {

    @Bean
    public Docket createRestApi() {
        return new Docket(DocumentationType.SWAGGER_2)
                .apiInfo(apiInfo())
                .select()
                .apis(RequestHandlerSelectors.basePackage("包名"))
                .paths(PathSelectors.any())
                .build();
    }

    private ApiInfo apiInfo() {
        return new ApiInfoBuilder()
                .title("xxx API")
                .version("1.0")
                .build();
    }
}
```

# Resource内容
## application.yml
```yml
spring:
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/数据库?serverTimezone=GMT
    password: 密码
    username: root
  jpa:
    show-sql: true
    hibernate:
      ddl-auto: update
  main:
    allow-bean-definition-overriding: true
```

# 要注意的细节
1. pom文件jdbc starter 和 mysql-connect-java starter添加错误
2. @Id    //导包问题 要导import javax.persistence.*;这个包
3. @ApiImplicitParam(name="page",value="字面意思",dataType="Integer", paramType = "query",example="1") name属性必须与参数名字一致 否则多重影分身
