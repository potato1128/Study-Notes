# mybatis-plus

## 1.sql打印日志配置

yml配置

```yml
mybatis-plus:
  configuration:
    log-impl: org.apache.ibatis.logging.stdout.StdOutImpl
```



## 2.表和列

### 2.1 主键类型

IdType的枚举类型如下

```java
public enum IdType {
    AUTO(0),
    NONE(1),
    INPUT(2),
    ID_WORKER(3),
    UUID(4),
    ID_WORKER_STR(5);

    private int key;

    private IdType(int key) {
        this.key = key;
    }

    public int getKey() {
        return this.key;
    }
}

```

0.auto自动增长(mysql,sql server)

1.none没有主键2.input手工输入
3.id_worker:实体类用Long id ，表的列用bigint , int类型大小不够
4.id_worker_str 实体类使用String id，表的列使用varchar 50
5.uuid 实体类使用String id，列使用varchar 50

### 2.2 指定表名

定义实体类，默认的表名和实体类同名

- 如果不一致，在实体类定义上面使用
  `@TableName(value=“数据库表名”)`

主要区别在于
定义实体类的时候使用的类名
如果不符合数据库表名要加上这个注解
数据库表名为user_address
![在这里插入图片描述](https://img-blog.csdnimg.cn/293df039d34e47adb61e94836a08c153.png)
