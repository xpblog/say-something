# [Maven命令启动springboot项目](https://github.com/xpblog/say-something/issues/14)

[返回目录](https://github.com/xpblog/say-something)

如果是用idea编写springboot项目，可以直接用idea启动。如果没有idea启动springboot项目就要借助maven插件了。

- 引入插件
 在pom.xml 文件中引入了 spring-boot-maven-plugin 插件依赖
```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
    </plugins>
</build>
```
- 启动项目
```java
mvn spring-boot:run
```
就可以启动项目了