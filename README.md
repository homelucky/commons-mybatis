# commons-mybatis

Mybatis通用数据层

通用`Mapper`, `Dao`, `Service`

适用于遵循`阿里巴巴java开发规范`的数据库表
- 表必备字段: `id`, `gmt_create`, `gmt_modified`
- `id`必为主键, 类型为`unsigned bigint`, 单表时自增, 步长为1
- `gmt_create`, `gmt_modified`的类型均为`date_time`类型
- 禁用保留字, 如`desc`、`range`、`match`、`delayed`... 请参考MySQL官方保留字
- 表名、字段名必须使用小写字母或数字, 禁止出现数字开头, 禁止两个下划线中间只出现数字

## 使用
简单编写实体类就可以使用了, 以下代码也可以使用代码生成器自动生成

[https://github.com/GitHub-Laziji/mybatis-generator](https://github.com/GitHub-Laziji/mybatis-generator)
模版选择`mybatis2`即可

### 引人
```
git clone https://github.com/GitHub-Laziji/commons-mybatis.git
cd commons-mybatis
mvn install
```
```XML
<dependency>
    <groupId>org.laziji.commons</groupId>
    <artifactId>commons-mybatis</artifactId>
    <version>2.0.0</version>
</dependency>
```


### 实体类
对于数据库user表
```Java
public class User extends BaseDO{
	private String username;
	private String password;
	//get set...
}
```
### 查询类
```Java
public class UserQuery extends BaseQuery<User> {

    private Long id;
    private Date gmtCreate;
    private Date gmtModified;
    private String username;
    private String usernameLike;
    private String password;
    private String passwordLike;
    //get set...
}
```

### Dao、Service
Dao和Service直接继承通用的基类 不需要写内容, 也不需要编写XML
```Java
@Mapper
public interface UserDao extends DODao<User> {

}
```
```Java
@Service
public class UserService extends BaseDOService<User> {

}
```

### 直接使用
```Java
@RestController
public class UserController {

    @Autowired
    private DOService<User> userService;

    @RequestMapping("/")
    public void index(){
        //userService.select(query)
        //userService.selectById(id)
        //userService.selectAll()
        //userService.selectCount(query)
        //userService.selectTotal()
        //userService.selectPage(query)
        //userService.update(bean)
        //userService.insert(query)
        //userService.delete(id)
    }
}
```