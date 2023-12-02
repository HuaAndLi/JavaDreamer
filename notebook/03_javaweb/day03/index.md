[TOC]



# 简介

第3天学习笔记



# JDBC

Java数据库连接

## JDBC体验

```java
    public static void main(String[] args) throws Exception {
        // 1.注册驱动
        // 2.获取连接
        Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/db1?useSSL=false", "root", "123456");
        System.out.println(conn);

        // 3.获取Statement
        Statement stmt = conn.createStatement(); // 小货车

        // 4.增加数据
        stmt.executeUpdate("INSERT INTO ACCOUNT (NAME, balance) VALUES ('抗得住', 99999999);");

        // 5.释放资源
        stmt.close();
        conn.close();
    }
```



## 数据库连接池

