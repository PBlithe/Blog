## Spring Boot页面显示问题

运行spring boot web项目时出现了This application has no explicit mapping for / error,so you are seeing this as a fallback.异常

某博客给出以下原因：

## 原因1:

**Application**启动类的位置不对.要将Application类放在最外侧,即包含所有子包 
原因:spring-boot会自动加载启动类所在包下及其子包下的所有组件.

## 原因2:

在springboot的配置文件:application.yml或application.properties中关于视图解析器的配置问题: 
当pom文件下的spring-boot-starter-paren版本高时使用: 
spring.mvc.view.prefix/spring.mvc.view.suffix 
当pom文件下的spring-boot-starter-paren版本低时使用: 
spring.view.prefix/spring.view.suffix

**在application.properties文件中添加以下内容**

```
spring.mvc.view.prefix=classpath:/templates/
spring.mvc.view.suffix=.html
```

## 原因3:

控制器的URL路径书写问题 
@RequestMapping(“xxxxxxxxxxxxxx”) 
实际访问的路径与”xxx”不符合.

排查了以上问题之后，我的浏览器仍然提示以上异常。后来我找出了问题所在。使用Thymeleaf模板时需要添加Thymeleaf依赖。

```xml
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-thymeleaf</artifactId>
 </dependency>
```

另附上如何用IDEA创建一个Spring Boot Web项目。

用IDEA构建了一个spring boot 的web项目。

1. ![1](C:\Users\zhizh\Desktop\新建文件夹\1.jpg)

   选择Spring Initializr,点击Next

2. ![2](C:\Users\zhizh\Desktop\新建文件夹\2.jpg)

   输入Group和Artifact的内容，点击Next

3. ![3](C:\Users\zhizh\Desktop\新建文件夹\3.jpg)

   选择Web和Spring Web Starter，点击Next

   项目就构建完了。

