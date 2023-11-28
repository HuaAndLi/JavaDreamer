[TOC]



# 简介

第13天学习笔记



# 单元测试

1.导入junit库

2.代码

```java
/**
    目标：使用Junit进行方法的正确性测试。
 */
public class UserServiceTest {

    @Before // 修饰实例方法
    public void before(){
        System.out.println("====before====");
    }

    @After // 修饰实例方法
    public void after(){
        System.out.println("====after====");
    }

    @BeforeClass // 修饰静态方法
    public static void beforeClass(){
        System.out.println("====beforeClass====");
    }

    @AfterClass // 修饰静态方法
    public static void afterClass(){
        System.out.println("====afterClass====");
    }



    /**
       注意：1、用public void修饰，不给参数的方法
            2、必须为这个测试方法加上一个注解@Test
     */
    @Test
    public void testLogin(){
        UserService userService = new UserService();
        String result =  userService.login("admin", "123456");
        // 断言：
        Assert.assertEquals("登录业务有人动过了","登录成功", result);
    }

    @Test
    public void testChu(){
        UserService userService = new UserService();
        userService.chu();
    }
}

```



# 反射

[二、java中反射的使用](https://blog.csdn.net/qq_38367575/article/details/121649638)

通过.class文件得到class对象，解析对象中的属性、方法等。

## 获取Class对象

- Class.forName(String className)
- 类名.class
- new 类().getClass()

```java
/**
    目标：反射第一步：获取Class对象
 */
public class ReflectDemo1 {
    public static void main(String[] args) throws Exception {
        // 1、第一步：Class下的静态方法forName(..)
        Class c1 = Class.forName("com.itheima.d2_reflect.Student");  // Student.class
        System.out.println(c1);

        // 2、类名.class
        Class c2 = Student.class;
        System.out.println(c2);

        // 3、对象获取Class对象
        Student s = new Student();
        Class c3 = s.getClass();
        System.out.println(c3);

        // 获取类名
        String name = c1.getName(); // 类的全名
        System.out.println(name);

        String name2 = c1.getSimpleName(); // 类的简名
        System.out.println(name2);

    }
}
```

## 获取构造器对象

```java
/**
    目标：获取Class对象中的构造器对象，并使用。（清楚它的API）
 */
public class ReflectDemo1 {
    @Test
    public void getAllConstructors(){
        // 1、反射第一步：得到Class对象
        Class c = Student.class;
        // 2、调用方法，得到全部构造器
        // getConstructors:只能获取全部public修饰的构造器。
        // Constructor[] constructors = c.getConstructors();

        // getDeclaredConstructors：获取全部申明的构造器，包括私有的构造器
        Constructor[] constructors = c.getDeclaredConstructors();
        // 3、遍历这些构造器对象
        for (Constructor constructor : constructors) {
            System.out.println(constructor.getName() + "---->" + constructor.getParameterCount());
        }
    }

    @Test
    public void getConstructor() throws Exception {
        // 1、反射第一步：得到Class对象
        Class c = Student.class;

        // 2、调用方法，得到某个构造器。
//        Constructor c1 = c.getConstructor(); // 只能拿空参数且public修饰的构造器对象 。
        Constructor c1 = c.getDeclaredConstructor(); // 只要申明的空参数构造器就可以拿到
        System.out.println(c1.getName() + "-->" + c1.getParameterCount());

        Constructor c2 = c.getDeclaredConstructor(String.class , int.class); // 定位有参数构造器，私有的一样可以拿
        System.out.println(c2.getName() + "-->" + c2.getParameterCount());
    }

    @Test
    public void createObj() throws Exception {
        // 1、反射第一步：得到Class对象
        Class c = Student.class;

        // 2、调用方法，得到某个构造器。
        Constructor c1 = c.getDeclaredConstructor(); // 只要申明的空参数构造器就可以拿到
        System.out.println(c1.getName() + "-->" + c1.getParameterCount());

        Constructor c2 = c.getDeclaredConstructor(String.class , int.class); // 定位有参数构造器，私有的一样可以拿
        System.out.println(c2.getName() + "-->" + c2.getParameterCount());

        // 3、无参数构造器创建对象(最终还是调用的无参数构造器)
        c1.setAccessible(true); // 暴露反射，强制打开权限访问私有的构造器：反射可以破坏封装性
        Student s1 = (Student) c1.newInstance();
        System.out.println(s1);

        // 4、有参数构造器创建一个对象
        Student s2 = (Student)c2.newInstance("猪八戒",1000);
        System.out.println(s2);
    }
}
```

## 获取成员变量

同之前链接

## 获取方法对象

同之前链接

# 注解

[一、JAVA中的注解使用](https://blog.csdn.net/qq_38367575/article/details/121648601)

# 动态代理

```java
/**
    作用：帮助我们生成业务对象的代理对象。
 */
public class ProxyUtil {
    public static <T> T getProxy(T obj) {
        // 返回一个代理对象，给别人使用。
        // Object newProxyInstance(ClassLoader loader, Class<?>[] interfaces, InvocationHandler h)
        // 参数一：类加载器,负责加载代理类的
        // 参数二：需要被代理的方法在哪些接口中。
        // 参数三：代理对象的核心处理逻辑
        return (T)Proxy.newProxyInstance(obj.getClass().getClassLoader(),
                obj.getClass().getInterfaces(), new InvocationHandler() {
                    @Override
                    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
                        // 核心处理逻辑
                        // proxy  代理对象：一般不需要理会。
                        // method 代表正在被代理的方法对象。
                        // args  被代理方法的参数值。
                        // 1、记录开始时间
                        long startTime = System.currentTimeMillis();
                        // 2、触发真正的业务对象的方法执行。
                        Object result = method.invoke(obj, args);
                        // 3、记录结束时间，统计耗时
                        long endTime = System.currentTimeMillis();
                        System.out.println(method.getName() + "方法耗时：" + (endTime - startTime) / 1000.0 + "s!");
                        return result; // 4、返回结果。
                    }
                });
    }
}
```













