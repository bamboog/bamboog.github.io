####  Xml_Schema
```
Spring 为基于 XML 构建的应用提供了一种扩展机制，用于定义和配置 Bean。
它允许使用者编写自定义的 XML bean 解析器，并将解析器本身以及最终定义的 Bean 集成到 Spring IOC 容器中。

编写一个 XML schema 文件描述的你节点元素。
编写一个 NamespaceHandler 的实现类
编写一个或者多个 BeanDefinitionParser 的实现 (关键步骤).
注册上述的 schema 和 handler。

```
