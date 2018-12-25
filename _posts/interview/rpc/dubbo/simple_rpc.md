#### SimpleRpc

#### 本质
- Server
  - 通信--> 反序列化 --》反射
- client
  - 动态代理-->序列化 --> 通信

#### 发展方向
- 序列化方式提升--- hesson,fastjson
- socket 通信提升 -netty mina
- 反射代理技术提升 --- javasist,cglib (对比试验)
- 服务注册发现--zk
- 重试，超时，负载


- 服务暴露
```java
  ServerSocket server = new ServerSocket(port);
  for(;;) {
    final Socket socket = server.accept();
    ObjectInputStream input = new ObjectInputStream(socket.getInputStream());
    Method method = service.getClass().getMethod(methodName, parameterTypes); //反射
    Object result = method.invoke(service, arguments);
  }                     
```

- 服务发现
```java
return (T) Proxy.newProxyInstance(interfaceClass.getClassLoader(), new Class<?>[] {interfaceClass}, new InvocationHandler() {
            public Object invoke(Object proxy, Method method, Object[] arguments) throws Throwable {
                Socket socket = new Socket(host, port);
                try {
                    ObjectOutputStream output = new ObjectOutputStream(socket.getOutputStream());
                    try {
                        output.writeUTF(method.getName());
                        output.writeObject(method.getParameterTypes());
                        output.writeObject(arguments);
                        ObjectInputStream input = new ObjectInputStream(socket.getInputStream());
                        try {
                            Object result = input.readObject();
                            if (result instanceof Throwable) {
                                throw (Throwable) result;
                            }
                            return result;
```
