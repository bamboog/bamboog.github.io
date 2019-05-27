### XML schema
- Spring 为基于 XML 构建的应用提供了一种扩展机制，用于定义和配置 Bean,用户可自定义 XML bean 解析器，解析自定义的格式，比如:
<dubbo:registry> ,<dubbo:protocol>

- 怎么实现：
  - XML schema 文件描述自定义bean
  - NamespaceHandler 的实现
  - BeanDefinitionParser 的实现
  - 注册上述的 schema，handler


1. 一个 resources/META-INF/xxx.xsd
2. XXXNameHander extends NamespaceHandlerSupport
3. XXX implements BeanDefinitionParser
4. resources/META-INF/spring.handlers  &  resources/META-INF/spring.schemas
