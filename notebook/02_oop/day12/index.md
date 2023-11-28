[TOC]



# 简介

第12天学习笔记

# 网络编程

为后面打基础

## 网络编程三要素

- ip   InteAddress
- port
- 协议

## UDP

```java
/**
     目标：学会UDP通信 - 快速入门。  需求：1发 1收。
     客户端 发送端、
 */
public class ClientDemo1 {
    public static void main(String[] args) throws Exception {
        // 1、创建一个发送端对象（人）:注意：发送端不用注册端口，存在默认端口
        DatagramSocket socket = new DatagramSocket();

        // 2、创建一个数据包对象，封装数据（韭菜盘子）
        /**
         DatagramPacket(byte buf[], int length,InetAddress address, int port)
         参数一：代表需要发送的字节数据。
         参数二：发送的字节数据的大小。
         参数三：对方的IP地址。
         参数四：对方服务器的端口号
         */
        byte[] buffer = "我是快乐的客户端，请问约吗？".getBytes();
        DatagramPacket packet = new DatagramPacket(buffer, buffer.length, InetAddress.getLocalHost(), 6666);

        // 3、发送数据包
        socket.send(packet);

        // 4、释放资源
        socket.close();
    }
}

/**
   服务端 接收端
 */
public class ServerDemo2 {
    public static void main(String[] args) throws Exception {
        System.out.println("服务端启动~~~");
        // 1、创建接收端对象（人）: 注意：接收端必须注册端口，别人才能找到这儿
        DatagramSocket socket = new DatagramSocket(6666);

        // 2、创建数据包对象（接韭菜的盘子）
        // public DatagramPacket(byte buf[], int length)
        byte[] buffer = new byte[64 * 1024];
        DatagramPacket packet = new DatagramPacket(buffer, buffer.length);

        // 3、接收数据包对象
        socket.receive(packet);
        // 得到读取的字节数量。
        int len = packet.getLength();
        System.out.println("每次读取的字节数为：" + len);

        // 4、把数据转换出来
        String rs = new String(buffer, 0, len);
        System.out.println("收到客户端发来的消息：" + rs);

        // 5、拿对方的IP地址。
        System.out.println("对方地址：" +packet.getSocketAddress());
        System.out.println("对方端口：" +packet.getPort());
    }
}

```





##  TCP

```java
/**
    目标：完成TCP通信客户端开发：实现发送一个消息出去。
 */
public class ClientDemo1 {
    public static void main(String[] args) throws Exception {
        // 1、创建一个Socket对象，请求与服务器的连接（TCP通信）
        Socket socket = new Socket("127.0.0.1", 9999);

        // 2、从socket通信管道中得到一个字节输出流，负责写数据出去
        OutputStream os = socket.getOutputStream();

        // 3、把低级字节输出流交给打印流
        PrintStream ps = new PrintStream(os);

        // 4、发送消息出去
        ps.println("我是客户端，我给你发了消息，约吗？");

        // 5、刷新
        ps.flush();
    }
}
/**
    目标：完成服务端代码的开发，实现接收一个消息。
 */
public class ServerDemo2 {
    public static void main(String[] args) throws Exception {
        System.out.println("服务端启动。。。");
        // 1、注册端口
        ServerSocket serverSocket = new ServerSocket(9999);

        // 2、开始等待接收客户端的socket连接请求
        Socket socket = serverSocket.accept();

        // 3、从socket通信管道中得到一个字节输入流读取数据
        InputStream is = socket.getInputStream();

        // 4、读取消息
        BufferedReader br = new BufferedReader(new InputStreamReader(is));

        // 5、读取一行消息。
        String line;
        if ((line = br.readLine()) != null) {
            System.out.println(socket.getRemoteSocketAddress() + "说了：" + line);
        }
    }
}
```





