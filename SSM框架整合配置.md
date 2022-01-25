

# SSM框架整合配置

## 1.前期准备

### 1.1 项目大概的目录结构

![image-20220104131402298](C:\Users\shuaiaf\AppData\Roaming\Typora\typora-user-images\image-20220104131402298.png)

**配置文件都要放在resources文件下！**

### 1.2 SSM中所需要的jar包依赖 pom.xml

```Maven
<!-- =============第一大类: Mybatis所需依赖===================-->
                 <!--Mybatis-->
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.2</version>
        </dependency>
        <!--mybatis-spring的整合包-->
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis-spring</artifactId>
            <version>2.0.2</version>
        </dependency>
            <!--Druid数据库连接池-->
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid</artifactId>
            <version>1.2.6</version>
        </dependency>
            <!--c3p0数据库连接池(和druid二选一)-->
        <dependency>
            <groupId>com.mchange</groupId>
            <artifactId>c3p0</artifactId>
            <version>0.9.5.3</version>
        </dependency>
       <!--用来支持事务-->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-jdbc</artifactId>
        <version>5.1.9.RELEASE</version>
    </dependency>
        <!--mysql数据库驱动-->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.47</version>
        </dependency>
        <!-- =============第二大类 :Springmvc所需依赖===================-->
                <!--Servlet -JSP -->
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>servlet-api</artifactId>
            <version>2.5</version>
        </dependency>
        <dependency>
            <groupId>javax.servlet.jsp</groupId>
            <artifactId>jsp-api</artifactId>
            <version>2.2</version>
        </dependency>
            <!--jstl标签库-->
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>jstl</artifactId>
            <version>1.2</version>
        </dependency>
        <!-- Spring5和Thymeleaf视图整合包 -->
        <dependency>
            <groupId>org.thymeleaf</groupId>
            <artifactId>thymeleaf-spring5</artifactId>
            <version>3.0.12.RELEASE</version>
        </dependency>

        <!--SpringMVC (springMvc依赖中有spring的传递依赖spring-context)-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>5.1.9.RELEASE</version>
        </dependency>
        <!-- =============第三大类 :其他依赖===================-->
        <!--导入log4j日志包,这三个必须依赖在一起!-->
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-api</artifactId>
            <version>1.8.0-beta0</version>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-log4j12</artifactId>
            <version>1.8.0-beta0</version>
        </dependency>
        <dependency>
            <groupId>log4j</groupId>
            <artifactId>log4j</artifactId>
            <version>1.2.17</version>
        </dependency>
        <!--Junit单元测试-->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
        </dependency>
    </dependencies>
```



### 1.3 Spring的总配置文件 applicationContext.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:util="http://www.springframework.org/schema/util"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/util https://www.springframework.org/schema/util/spring-util.xsd">
        <import resource="classpath:spring-dao.xml"/>
        <import resource="classpath:spring-service.xml"/>
        <import resource="classpath:spring-mvc.xml"/>
    </beans>
```

  <import resource="classpath:spring-dao.xml"/>
        <import resource="classpath:spring-service.xml"/>
        <import resource="classpath:spring-mvc.xml"/>

**将其他的配置文件交给spring的总配置文件来管理(也可以写在一起，这里只是拆分了，以便于更直观！)**

### 1.4 Mybatis的配置文件 Mybatis-config.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
      <!--    是否开启驼峰命名自动映射，即从经典数据库列名 A_COLUMN 映射到经典 Java 属性名 aColumn-->
      <settings>
         <setting name="mapUnderscoreToCamelCase" value="true"/>


         <setting name="logImpl" value="LOG4J"/>
      </settings>
      <!--    分页插件注册-->     
<!--      <plugins>-->
<!--         <plugin interceptor="com.github.pagehelper.PageInterceptor">-->
<!--            <property name="param1" value="value1"/>-->
<!--         </plugin>-->
<!--      </plugins>-->
   <mappers>
    <mapper resource="mapper/BookMapper.xml"></mapper>
    <mapper resource="mapper/UserMapper.xml"></mapper>
</mappers>
</configuration>
```

 mapper：mapper下面有三个属性 class，url，resources 

1. 当xx**mapper.xml**映射文件在dao层下面，用class直接写xxmapper的路径

   <mapper class="potato/dao/BookMapper"></mapper>

    2.如果放在resource下的mapper包下，则写xxmapper.xml的路径

    <mapper resource="mapper/xxMapper.xml"></mapper>

***这里只需要注册mapper文件其余的都交给整合文件处理！***

### 1.5 web.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    <!--编码过滤器,要写在DispatcherServlet前面！-->
    <filter>
        <filter-name>encodingFilter</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
            <param-name>encoding</param-name>
            <param-value>utf-8</param-value>
        </init-param>
    </filter>
    <filter-mapping>
        <filter-name>encodingFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
       <!--DispatcherServlet-->
    <servlet>
        <servlet-name>DispatcherServlet</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <!--一定要注意:我们这里加载的是总的配置文件，之前被这里坑了！-->
            <param-value>classpath:applicationContext.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>DispatcherServlet</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>

</web-app>
```

## 2.整合文件

### 2.1 Spring-Mybatis整合 spring-dao.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">

    <!-- 配置整合mybatis -->
    <!-- 1.关联数据库文件 -->
    <!-- 2.数据库连接池 -->
    <!--数据库连接池
        dbcp  半自动化操作  不能自动连接
        c3p0  自动化操作（自动的加载配置文件 并且设置到对象里面）
    -->
    <context:property-placeholder location="classpath:databases.properties"/>
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
        <!-- 配置连接池属性 -->
        <property name="driverClassName" value="${jdbc.driver}"/>
        <property name="url" value="${jdbc.url}"/>
        <property name="username" value="${jdbc.username}"/>
        <property name="password" value="${jdbc.password}"/>
    </bean>
    <!-- 3.配置SqlSessionFactory对象 -->
    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <!-- 注入数据库连接池 -->
        <property name="dataSource" ref="dataSource"/>
<!--        &lt;!&ndash; 配置MyBaties全局配置文件:mybatis-config.xml &ndash;&gt;-->
        <property name="configLocation" value="classpath:mybatis-config.xml"/>
    </bean>
    <!-- 4.配置扫描Dao接口包，动态实现Dao接口注入到spring容器中 -->
    <!--解释 ：https://www.cnblogs.com/jpfss/p/7799806.html-->
    <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer" >
                  <property name="basePackage" value="potato.dao" />
                 <property name="sqlSessionFactoryBeanName" value="sqlSessionFactory" />
         </bean>
</beans>
```

#### 数据库连接配置文件  databases.properties

```java
jdbc.driver=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/ssm?useSSL=false&useUnicode=true&characterEncoding=utf8
jdbc.username=root
jdbc.password=123456
```

### 2.2 Spring-mvc整合 spring-mvc.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans.xsd
    http://www.springframework.org/schema/context
    http://www.springframework.org/schema/context/spring-context.xsd
    http://www.springframework.org/schema/mvc
    https://www.springframework.org/schema/mvc/spring-mvc.xsd">
    <!-- 4.扫描controller控制器 -->
    <context:component-scan base-package="potato.controller" />
    <!-- 配置SpringMVC 的视图控制器-->

    <!-- 1.开启SpringMVC注解驱动 -->
    <mvc:annotation-driven />
    <!-- 2.静态资源默认servlet配置-->
    <mvc:default-servlet-handler/>

    <!-- 3.配置jsp 显示ViewResolver视图解析器 -->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="viewClass" value="org.springframework.web.servlet.view.JstlView" />
        <property name="prefix" value="/WEB-INF/jsp/" />
        <property name="suffix" value=".jsp" />
    </bean>
<!--     二选一！-->
<!--    &lt;!&ndash; 3.配置 html Thymeleaf视图解析器 &ndash;&gt;-->
<!--    <bean id="resolver" class="org.thymeleaf.spring5.view.ThymeleafViewResolver">-->
<!--        <property name="order" value="1"></property>-->
<!--        <property name="characterEncoding" value="UTF-8"/>-->
<!--        <property name="templateEngine">-->
<!--            <bean class="org.thymeleaf.spring5.SpringTemplateEngine">-->
<!--                <property name="templateResolver">-->
<!--                    <bean class="org.thymeleaf.spring5.templateresolver.SpringResourceTemplateResolver">-->
<!--                        <property name="prefix" value="/WEB-INF/templates/"/>-->
<!--                        &lt;!&ndash; 视图后缀 &ndash;&gt;-->
<!--                        <property name="suffix" value=".html"/>-->
<!--                        <property name="templateMode" value="HTML5"/>-->
<!--                        <property name="characterEncoding" value="UTF-8" />-->
<!--                    </bean>-->
<!--                </property>-->
<!--            </bean>-->
<!--        </property>-->
<!--    </bean>-->

</beans>
```

### 2.3 Spring-Service整合 spring-service.xml

***Service层注入mapper可以用注解，但更推荐配置文件方式！***

***事务控制与aop也在这里处理，这样只是更分离了***

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans.xsd
    http://www.springframework.org/schema/context
    http://www.springframework.org/schema/context/spring-context.xsd">

    <!-- 扫描service相关的bean -->
    <context:component-scan base-package="potato.service" />

<!--    BookServiceImpl注入到IOC容器中-->
    <bean id="BookServiceImpl" class="potato.service.BookServiceImpl">
        <property name="bookMapper" ref="bookMapper"/>
    </bean>
    <!-- 配置事务管理器 -->
    <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <!-- 注入数据库连接池 -->
        <property name="dataSource" ref="dataSource" />
    </bean>
</beans>
```



### 2.4 日志文件 log4j.properties

```java
# Set root logger level to DEBUG and its only appender to A1.
log4j.rootLogger=DEBUG, A1

# A1 is set to be a ConsoleAppender.
log4j.appender.A1=org.apache.log4j.ConsoleAppender

# A1 uses PatternLayout.
log4j.appender.A1.layout=org.apache.log4j.PatternLayout
log4j.appender.A1.layout.ConversionPattern=%-4r [%t] %-5p %c %x - %m%n
```



大功告成！
