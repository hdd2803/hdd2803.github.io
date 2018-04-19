---
layout: post
title: Spring注解汇总
date: 2017-11-10 
tag: JavaNote
---

### 一、元注解
1、@Documented：表示含有此注解的注解应该被Javadoc工具记录，默认注解是不记录的。

2、@Inherited：表示含有此注解的注解可以被子类继承，只能用在类上。

3、@Retention(RUNTIME)：表示含有此注解的注解会保留到哪个。 例如：
- SOURCE--只在源代码级别保留，编译时就会被忽略。
- CLASS--编译时被保留，在class文件中存在，但JVM将会忽略。
- RUNTIME--将被JVM保留，所以他们能在运行时被JVM或其他使用反射机制的代码所读取和使用。

4、@Target({TYPE, METHOD, FIELD, PARAMETER})：表示含有此注解的注解使用范围。
[](/images/posts/JavaNote/SpringAnnotation/1.png)

### 二、Bean类注解
1、@Component：将类标记为一个组件，以Bean的形式注入到Spring容器中。相当于xml配置中的`<bean id="" class=""/>`。bean的ID默认为将类名第一个字母变为小写的字符串。

2、@ComponentScan：会默认扫描与配置类相同的包，将扫描到的@Component类自动注入到Spring容器中，免去写@Bean方法。

3、@Autowired：为属性或方法的形参自动注入bean，默认按类型装配，属于Spring的注解。

4、@Resource：为属性或方法的形参自动注入bean，默认按名称装配，若按名称找不到，则切换按类型装配，属于J2EE的注解。也可以写在类上，表示这是一个bean，而@Autowired不能。

5、@Bean：标记此方法返回一个bean，一般用在@Configuration类中。bean的ID默认和带有@Bean注解的方法名是一样的。

6、@Configuration：标记此类为一个配置类，自动将类中的@Bean下的类注入到Spring容器中。

7、@Controller：声明一个controller类bean。（注入service）

8、@Service：声明一个service类bean。（注入dao）

9、@Repository：声明一个dao类bean。（实现数据访问，常与Hibernate使用）

10、@ConditionOnMissingBean：当bean不存在时，才创建bean，常放在@Bean下面。

11、@Conditional（xxx.class）：指定创建bean的条件类，若条件类的matches()返回true则创建此bean。

12、@Primary：指定那个bean为子类中首选的bean。

13、@Qualifier（xxx）：指定bean的别名。

14、@Scope（xxx）：指定bean的作用域。一共有单例、原型、会话、请求四种作用域，例
如：@Scope(ConfigurableBeanFactory.SCOPE_SINGLETON)。

15、@Mapper：使Mapper类接口与Mapper.xml文件相互映射，实现数据访问功能。例如：WallMapper.java接口和WallMapper.xml相对应，从而实现里面的数据访问方法。（实现数据访问，常与Mybatis使用）

16、@MapperScan（xxx）：指定扫描Mapper类接口的包。例如：@MapperScan（"com.dong.mapper"）。

17、@Valid：验证后面的形参是否满足校验类注解的要求。通常用在形参为POJO的对象上。

18、@PathVariable：将URL中占位符参数绑定到控制器处理方法的形参中。例如：URL中的/user/{xxx}通过@PathVariable("xxx") 绑定到操作方法的形参中。

19、@Transactional：声明方法或类中的方法以事务的方式运行。

20、@EnableTransactionManagement：开启类以事务方式运行其中的方法。

### 三、请求类注解
1、@EnableWebMVC：启用MVC。

2、@RequestParam：指定参数的一些属性，比如required（是否必须）、value（对应请求体中的参数）、defaultValue（默认值）。例如：
```
@RequestParam(value = "age", required = true, defaultValue = "23") String userAge。
```

3、@RequestMapping（xxx）：指定访问的路径，可用在方法和类上。可以限制路径、请求类型、接收参数、接收请求头，例如：
```
@RequestMapping(value="/login", method=RequestMethod.POST, params="name", headers="Content-Type:text/html;charset=UTF-8")
```

4、@GetMapping（xxx）：指定接受GET请求及其请求路径。

5、@POSTMapping（xxx）：指定接受POST请求及其请求路径。

6、@RequestBody：用来解析content-type不是application/x-www-form-urlcoded类型的请求内容，并自动编码为指定的形参类。

7、@ResponseBody：用于将Controller的方法返回的对象，根据HTTP Request Header的Accept的内容，通过适当的HttpMessageConverter转换为指定格式后，写入到Response对象的body数据区。使用时，返回的数据不是html标签的页面，而是其他某种格式的数据时（如json、xml等）使用。

8、@RequestHeader：可将请求头中的属性值绑定到处理方法的形参中。

9、@CookieValue：获取cookie值，有value、required、defaultValue三个参数。

### 四、资源类注解
1、@Import（xxx.class）：指定需要导入的类。

2、@ImportResource（xxx）：指定需要导入的文件。

3、@Profile（xxx）：指定使用哪个配置文件。

4、@ActiveProfile（xxx）：指定运行时需要激活哪一个配置文件。

5、@PropertySource（xxx）：隔离加载配置文件。例如：
```
@PropertySource("classpath:/com/sound/app/properties")。
```

### 五、辅助类注解
1、@Override：指定此方法被子类重写。加上此注解可以确认方法是否写对，若写错会报错。

2、@SuppressWarnings(xxx)：屏蔽某些编译时的警告信息。例如：
- @SuppressWarnings("unused") 屏蔽方法或对象从未使用的警告。
- @SuppressWarnings("rawtypes") 屏蔽对象未使用泛型指定类型的警告。
- @SuppressWarnings("deprecation")屏蔽使用了已过时或者不推荐使用的类或方法时的警告。
- @SuppressWarnings("unchecked") 屏蔽未执行类型转换检查的警告。
- @SuppressWarnings("fallthrough") 屏蔽当Switch程序块直接通往下一种情况而没有Break时的警告。
- @SuppressWarnings("path") 屏蔽在类、源文件等路径中有不存在的路径时的警告。
- @SuppressWarnings("serial") 屏蔽当在可序列化的类上缺少serialVersionUID定义时的警告。
- @SuppressWarnings("all") 屏蔽所有情况的警告。

### 六、测试类注解
1、@RunWith（xxx.class）：指定类运行时需要依赖的测试类。

2、@ContextConfiguration（classes=xxx.class）：指定需要加载的配置类。

3、@Test：标记测试的方法。

### 七、切面类注解
1、@AspectJ：标记此类为切面。

2、@Pointcut：声明切点方法。

3、@Before：通过方法会在目标方法调用之前执行。

4、@After：通知方法会在目标方法调用之后执行。

5、@AfterThrowing：通知方法会在目标方法抛出异常后调用。

6、@AfterReturning：通知方法会在目标方法返回后调用。

7、@Around：通知方法会将目标方法封装起来。

8、@EnableAspectJAutoProxy：启用AspectJ自动代理。

### 八、校验类注解
1、空检查

1）@Null：验证对象是否为null。

2）@NotNull：验证对象是否不为null, 无法查检长度为0的字符串。

3）@NotBlank：检查约束字符串是不是Null还有被Trim的长度是否大于0,只对字符串,且会去掉前后空格。

4）@NotEmpty：检查约束元素是否为NULL或者是EMPTY。

2、Booelan检查

1）@AssertTrue：验证 Boolean 对象是否为 true。  

2）@AssertFalse：验证 Boolean 对象是否为 false。  

3、长度检查

1）@Size(min=, max=)：验证对象（Array,Collection,Map,String）长度是否在给定的范围之内。  

2）@Length(min=, max=)：验证string的长度是否在给定范围之内。

4、日期检查

1）@Past：验证 Date 和 Calendar 对象是否在当前时间之前。  

2）@Future：验证 Date 和 Calendar 对象是否在当前时间之后。

3）@Pattern：验证 String 对象是否符合正则表达式的规则。

5、数值检查。建议使用在Stirng,Integer类型，不建议使用在int类型上，因为表单值为"
"时无法转换为int，但可以转换为Stirng为""，Integer为null。

1）@Min：验证 Number 和 String 对象是否大等于指定的值 。

2）@Max：验证 Number 和 String 对象是否小等于指定的值 。

3）@DecimalMax：被标注的值必须不大于约束中指定的最大值.这个约束的参数是一个通过
BigDecimal定义的最大值的字符串表示。小数存在精度。

4）@DecimalMin：被标注的值必须不小于约束中指定的最小值.这个约束的参数是一个通过
BigDecimal定义的最小值的字符串表示。小数存在精度。

5）@Digits：验证 Number 和 String 的构成是否合法  。

6）@Digits(integer=,fraction=)验证字符串是否是符合指定格式的数字，interger指定整数精度，fraction指定小数精度。

7）@Range(min=, max=) 检查数字是否介于min和max之间。例如：
```
@Range(min=10000,max=50000,message="range.bean.wage")private BigDecimal wage;
```

8）@Valid：递归的对关联对象进行校验，如果关联对象是个集合或者数组，那么对其中的元素进行递归校验；如果是一个map，则对其中的值部分进行校验。(是否进行递归验证)

9）@CreditCardNumber：信用卡验证。

10）@Email：验证是否是邮件地址，如果为null,不进行验证，算通过验证。

11）@ScriptAssert(lang= , script=, alias=)：验证调用的脚步。

12）@URL(protocol=, host=, port=, regexp=, flags=)：验证URL。

#### 备注：
1、xxx.class指某个类名。

2、xxx指某个字符串。


<br>
转载请注明：[Dong的博客](http://hdd2803.github.io) » [Spring注解汇总](http://hdd2803.github.io/2017/11/JavaNote_Spring注解汇总/)
